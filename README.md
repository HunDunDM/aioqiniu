# aioqiniu

[![][qiniu_logo]](https://www.qiniu.com)

![][version] ![][license] ![][python]

`aioqiniu`是基于`asyncio`和`aiohttp`的七牛云Python异步客户端库。

## Install

```bash
$ sudo pip3 install aioqiniu
```

## Requirements

* Python &gt;= 3.5
* qiniu
* aiohttp

## Getting started

使用样例：获取文件元信息

```python
import asyncio

import aioqiniu

async def main():
    client = aioqiniu.QiniuClient("MY_ACCESS_KEY", "MY_SECRET_KEY")
    stat = await client.get_file_stat("BUCKET_NAME", "FILE_NAME")
    print(stat)

if __name__ == "__main__":
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
```

## Documentation

直接在Python中通过`help`来查看`aioqiniu`的API文档。

更多API细节可查看注释中提供的七牛官方文档地址。

## Tests

本项目使用`pytest`做单元测试，运行测试需要安装以下依赖

* `pytest`
* `pytest-asyncio`

运行下面的命令安装运行测试所需的依赖

```bash
$ sudo pip3 install pytest pytest-asyncio
```

在该项目根目录下执行以下命令来运行测试

```bash
$ pytest
```

**注意**：部分测试需要设置环境变量`QINIU_ACCESS_KEY`和`QINIU_SECRET_KEY`才会运行

## Changelog

* `v1.2.0`(2017-05-10)

    * `aioqiniu.utils`模块添加计算七牛etag相关的工具函数

        * `get_stream_etag`

            从一个流中读取数据并计算七牛etag

        * `get_data_etag`

            从字节码数据中计算七牛etag

        * `get_file_etag`

            从本地文件中读取数据计算七牛etag

    * `QiniuClient`添加从原始数据中计算token的一些相关方法，用于替代`qiniu.Auth`的相关功能

        * `get_token`

            根据原始数据生成token，同`qiniu.Auth.token`

        * `get_token_with_data`

            根据原始数据生成含已编码原始数据的token，同`qiniu.Auth.token_with_data`

    * 添加生成私有资源url的方法`QiniuClient.get_private_download_url`

* `v1.1.0`(2017-05-05)

    * API`QiniuClient.get_encoded_entry_uri`转移到新模块`aioqiniu.utils`中作为一个函数来使用

    * 添加批量操作的API`QiniuClient.batch`

    * 添加直传本地文件的API`QiniuClient.upload_file`

    * 更改`QiniuClient.upload_data`方法的参数名，使API调用更加方便

        * `upload_token -> token`
        * `upload_host -> host`

    * 更换`QiniuClient.upload_data`API的`data`和`token`的参数位置，调用更符合直觉，现在是这样调用

        ```python
        await qiniuclient.upload_data(data, token, ...)
        ```

* `v1.0.0`(2017-05-03)

    基于`asyncio`和`aiohttp`的七牛云Python异步客户端库。

    支持以下API：

    * 查询、创建和删除空间
    * 查询空间绑定的域名列表
    * 查找、上传和删除文件
    * 拷贝、移动和重命名文件
    * 修改文件MIME类型信息
    * 设置文件的生命周期
    * 镜像回源预取
    * 第三方资源抓取
    * 其它主要是内部使用的API（非协程API，主要是生成token以及相关的数据格式）

[qiniu_logo]: http://assets.qiniu.com/qiniu-204x109.png
[version]: https://img.shields.io/badge/version-1.2.0-blue.svg
[license]: https://img.shields.io/badge/license-MIT-blue.svg
[python]: https://img.shields.io/badge/python-%3E%3D3.5-blue.svg
