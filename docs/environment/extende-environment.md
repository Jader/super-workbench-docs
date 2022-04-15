# 扩展环境

## 扩展 extend 环境程序

### 调整编排

`docker-compose.yml` 中 `extend` 服务增加 `volumes`，增加对应程序目录配置。可以参考会议、日程模块

> 其中 `EXTEND_VENDOR_PATH`、`EXTEND_MEETING_PATH` 属于新增挂载项

### 增加 .env 配置

在原有基础上新增 `EXTEND_*_PATH` 变量，其中 `*` 表示为要扩展的程序标识。可以参考会议、日程模块

### 增加 nginx 配置

修改 `nginx/extend` 目录下 `apps.conf` 文件，添加一下对应程序转发规则。可以参考会议、日程模块

> 如果需要本地快调试，不搭配云助手可以增加对应项目的 `nignx` 配置。可以参考会议、日程模块

### 重新编排

```
$ docker-compose down
$ docker-compose up -d
```