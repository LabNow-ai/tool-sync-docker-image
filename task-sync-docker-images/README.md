# Understanding the docker images sync process

如果需要手工来操作，可以在该目录下创建一个认证文件，例如：

```auth.json
{
  "docker.io": {
    "username": "<your-docker-io-username>",
    "password": "<your-docker-io-password>",
    "insecure": true
  },
  "quay.io": {
    "username": "<your-quay-io-username>",
    "password": "<your-quay-io-password>",
    "insecure": true
  },
  "registry.cn-beijing.aliyuncs.com" : {
    "username": "<your-aliyun-acr-username>",
    "password": "<your-aliyun-acr-password>"
  },
  "registry.cn-hangzhou.aliyuncs.com" : {
    "username": "<your-aliyun-acr-username>",
    "password": "<your-aliyun-acr-password>"
  }
}
```
