# 超级工作台本地环境搭建

## 安装依赖工具

- Git
- Docker [https://docs.docker.com/install/]
- Docker-compose [https://docs.docker.com/compose/install/#install-compose]

## 获取部署脚本

```bash
$ git clone https://github.com/Jader/SuperWorkbenchDock.git
```

## 调整配置

```bash
$ cd SuperWorkbenchDock.git   // 进入项目根目录
$ cp .env.example .env  // 配置相关选项
```

> 具体配置相关说明可以看下 `.env.example` 文件中的注视说明。复制出 `.env` 文件后，根据个人喜好调整即可

*网关相关配置可默认，也自行修改*
*默认环境域名为 `szgzt.me`，如果需要调整可以修改项目根目录下 `nginx` 目录中的配置项即可*

## hosts 配置

根据系统不同自行调整本机 `hosts` 文件，域名根据上面配置自行调整

```
127.0.0.1 site.szgzt.me back.szgzt.me 
127.0.0.1 front.szgzt.me priv.szgzt.me cyjs_demo.front.szgzt.me
127.0.0.1 extend.szgzt.me back.meeting.me front.meeting.me back.schedule.me
```

域名清单

| 域名 | 说明 |
|:--|---|
| site.szgzt.me | 超级工作台企业管理后台 |
| back.szgzt.me | 数字工作台后台，本地开发可用，site域携带/gzt 时会被重定向到 back 域 |
| front.szgzt.me | 超级工作台前台 |
| priv.szgzt.me | 超级工作台预览 |
| cyjs_demo.front.szgzt.me | cyjs_demo 租户超级工作台前台 |
| extend.szgzt.me | 云助手后台 |
| back.meeting.me | 会议后台，本地开发可用 |
| front.meeting.me | 会议前台，本地开发可用 |
| back.schedule.me | 日程后台，本地开发可用 |
| front.schedule.me | 日程前台，本地开发可用 |

## 运行容器编排

同时运行超级工作台服务和会议、日程服务

```bash
$ docker-compose up -d
```

只想单独运行超级工作台服务

```bash
$ docker-compose up super-workbench -d
```

只想单独运行云助手、会议、日程服务

> **注意：**该容器服务使用81端口映射、如果需要请调整 `docker-compose.yml` 中 `extend` 容器 `ports` 值

```bash
$ docker-compose up extend -d
```

## 容器说明

| 容器名 | 说明 |
|:--|---|
| super-workbench | 运行超级工作台程序环境，默认端口为80，`php` 版本为 `7.4.26` |
| extend | 运行云助手、会议、日程相关程序环境、默认端口为81，`php` 版本为 `5.6.40` |

> 如果需要用到 `https` 可以自行生成 ssl 证书引入并增加 `443` 端口映射

## Todo

- [ ] 目前 `SuperWorkbenchDock` 前端项目未全部添加上，后端计划任务相关也未添加，总体运行上不影响日常开发
- [ ] 前后端分离，目前前后端代码统一编排成一个容器运行