# uptime-status

一个基于 UptimeRobot API 的在线状态页面，本项目二改自 [yb/uptime-status](https://github.com/yb/uptime-status)。

<img width="1152" alt="image" src="https://user-images.githubusercontent.com/25887822/178935137-6d23521d-5894-4fb8-922d-3575be4f7abc.png">

## 先决条件

- 您需要先到 [UptimeRobot](https://uptimerobot.com/ "UptimeRobot") 添加站点监控，并在 My Settings 页面获取 API Key
- 您需要拥有一个网站空间，常见的 Nginx / PHP 等空间即可，甚至是阿里云的 OSS 等纯静态空间也行

## 部署
### Vercel（推荐）

- 在右上角Fork此存储库，然后在 Vercel 部署。完成后，你需要在Fork的存储库中编辑配置文件。
- 修改 `config.js` 文件：
   - `SiteName`: 要显示的网站名称
   - `ApiKeys`: 从 UptimeRobot 获取的 API Key，支持 Monitor-Specific API Keys 和 Read-Only API Key
   - `CountDays`: 要显示的日志天数，建议 60 或 90，显示效果比较好
   - `ShowLink`: 是否显示站点链接
   - `Navi`: 导航栏的菜单列表
- 大功告成！你可以在项目>设置>域名中绑定自己的域名，获得更好的访问速度。

### COS或静态空间
- 下载并解压最新版本：[uptime-status.zip](https://github.com/Andy17269/uptime-status/releases/latest/download/uptime-status.zip "uptime-status.zip") 
- 修改 `config.js` 文件：
   - `SiteName`: 要显示的网站名称
   - `ApiKeys`: 从 UptimeRobot 获取的 API Key，支持 Monitor-Specific API Keys 和 Read-Only API Key
   - `CountDays`: 要显示的日志天数，建议 60 或 90，显示效果比较好
   - `ShowLink`: 是否显示站点链接
   - `Navi`: 导航栏的菜单列表
- 将所有文件上传到COS

⚠️ 如果没有修改代码的需求，您不需要 clone 本项目，只需要下载 Release 的文件包即可。

## 接口代理

对于想自己搭建接口的代理的，可以参考以下 nginx 的配置文件：

```
server {
  listen [::]:80;
  server_name cors.status.org.cn;
  location / {
    proxy_ssl_server_name on;
    proxy_pass https://api.uptimerobot.com/;
    proxy_hide_header Access-Control-Allow-Origin;
    add_header Access-Control-Allow-Origin * always;
  }
}
```
