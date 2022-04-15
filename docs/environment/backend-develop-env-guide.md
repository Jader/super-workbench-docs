# 后端开发环境配置问题指南

## 镜像更换 

`super-workbench` 容器使用的镜像为 [`jaderh/docker-nginx-php-supervisor:vat`](https://github.com/Jader/docker-nginx-php-supervisor/tree/vat)，可参考源码自行修改，修改只需调整 `docker-compose.yml` 文件中 `super-workbench` 下 `image` 值。

`extend` 容器使用的镜像为 [`jaderh/docker-nginx-php-supervisor:plan`](https://github.com/Jader/docker-nginx-php-supervisor/tree/plan)，可参考源码自行修改，修改只需调整 `docker-compose.yml` 文件中 `extend` 下 `image` 值。

## 前端项目

由于后端开发过程中很少关注或修改前端代码，所以为防止前端占用电脑资源，建议使用前端构建模式生成静态文件，前端项目分支建议使用 `T1` 分支；保证构建和测试环境一致。

### enterprise-frontend 编译命令

*`yarn` 命令也可以替换为 `npm`*

```bash
$ cd ${APPS_FRONT_PATH}
$ yarn install --registry "https://npm.mingyuanyun.com/"
$ yarn build
```


### enterprise-frontend 编译命令

*`yarn` 命令也可以替换为 `npm`*

```bash
$ cd ${SZGZT_FRONT_PATH}/frontend
$ yarn install --registry "https://npm.mingyuanyun.com/"
$ yarn build
```

> 本地 `node` 版本如果大于等于 16，可能会出现编译错误。目前已知出现 `DeprecationWarning: In future versions of Node.js, fs.rmdir(path, { recursive: true }) will be removed. Use fs.rm(path, { recursive: true }) instead`，可以调整 `szgzt-web/frontend/build/prod/build-widgets.js` 文件中 `fs.promises.rmdir` 方法为 `fs.promises.rm`