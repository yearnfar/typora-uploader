# typora-uploader

typora-uploader 支持在 Typora 工具中上传图片资源到 AWS S3

![Typora设置](./assets/example.png)

### Feature

- 上传到 AWS S3
- 上传到 Aliyun OSS
- 支持上传后根据定义模版修改文件名
- 支持 png、jpg 文件转 webp

### Install

```shell
pip install -r requirement.txt
```

### Usage

默认加载 main.py 所在目录的 config.json 配置，也可以通过 --config 指定配置文件:

```shell
python main.py file1.txt file2.txt

python main.py --config CONFIG_DIR/config.json file1.txt file2.txt
```

### config.json

| 字段              | 说明                | 示例                                  |
| ----------------- | ------------------- | ------------------------------------- |
| type              | 类型，支持 s3, oss  | "s3" 或 "oss"                         |
| region            | 区域                | "ap-southeast-1" 或 "oss-cn-hangzhou" |
| image_to_webp     | 图片转为 webp       | true                                  |
| base_url          | 自定义 URL          | "https://www.example.com"             |
| bucket_name       | 桶名称              | "my-bucket"                           |
| object_key        | object key 格式模版 | "{year}/{month}/{file_md5}.{ext}"     |
| access_key_id     | access_key_id       | ""                                    |
| access_key_secret | access_key_secret   | ""                                    |

#### object_key 支持下列可替换字符:

- filename": 文件名称，含后缀
- name": 文件名称，不含后缀
- ext": 文件后缀，不含.，例如: png
- timestamp": 时间戳
- full_year": 年，例如：2025
- full_month": 月，01~12
- full_day": 天，01~31
- year": 年，2 位数，例如：25
- month":月，1~12，不含 0
- day": 天，不含 1~31，不包含 0
- datetime_second": 年月日时分秒，例如：20250410125959
- file_md5: 文件的 md5 值

```json
{
  "type": "oss",
  "image_to_webp": true,
  "base_url": "https://www.example.com",
  "region": "",
  "bucket_name": "my-bucket",
  "object_key": "{year}/{month}/{file_md5}.{ext}",
  "access_key_id": "",
  "access_key_secret": ""
}
```
