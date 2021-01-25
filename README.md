云函数快速部署京东脚本


本地安装依赖使用serverless部署，点这里

Github Action 部署点这里




1. 安装 Node.js 环境
Node.js 环境 下载地址 ，根据自己的操作系统下载和安装。

2. 下载代码
点击红框处下载压缩包


3. 安装依赖，配置 cookie

3.1 安装依赖
压缩包解压后进入项目文件夹

Windows 用户按住  shift 点击右键，点击 在此处打开命令窗口

Mac 用户通过终端，自行进入该文件夹

在命令行内输入 npm i ，等待运行完成。
此时，项目文件夹内会多出一个 node_modules文件夹

3.2 配置 cookie
打开项目文件内的 jdCookie.js
在最上面的 CookieJDs里写入 cookie ，多个账号以逗号分隔
例如
let CookieJDs = [
  'pt_key=xxx;pt_pin=xxx;', 
  'pt_key=zzz;pt_pin=zzz;',
  'pt_key=aaa;pt_pin=xxxaaa'
]

注：获取京东 cookie 教程参考 浏览器获取京东cookie教程 , 插件获取京东cookie教程


4. 部署到云函数

4.1 开通服务
依次登录 SCF 云函数控制台 和 SLS 控制台 开通相关服务，确保账户下已开通服务并创建相应服务角色 SCF_QcsRole、SLS_QcsRole

注意！为了确保权限足够，获取这两个参数时不要使用子账户！此外，腾讯云账户需要实名认证。


4.2 工具部署
下载 Serverless 工具，快速部署函数
npm install -g serverless
执行部署命令
serverless deploy
如果已经配置了永久秘钥，则可以直接部署，如果没有，可以直接微信扫码登录腾讯云，并且授权部署。
过几秒后，查看输出，可以看到函数和定时触发器都已经配置完成。
serverless ⚡framework
Action: "deploy" - Stage: "dev" - App: "jdscript" - Instance: "jdscript"

functionName: scf-jdscript
description:  This is a function in jdscript application.
namespace:    default
runtime:      Nodejs12.16
handler:      index.main_handler
memorySize:   64
lastVersion:  $LATEST
traffic:      1
triggers: 
  timer: 
    - timer-jdscript-dev

36s › jdscript › Success

5. 查看和测试
登录后，在 腾讯云函数地址 点击管理控制台，查看最新部署的函数。
在左侧栏的日志查询中，可以查看到触发的日志，包括是否打卡成功等。


如果需要配置永久秘钥，则可以在访问秘钥页面获取账号的 TENCENT_SECRET_ID，TENCENT_SECRET_KEY，并配置在代码根目录 .env 文件中。


Github Action 部署

1. 开通服务
依次登录 SCF 云函数控制台 和 SLS 控制台 开通相关服务，确保账户下已开通服务并创建相应服务角色 SCF_QcsRole、SLS_QcsRole

注意！为了确保权限足够，获取这两个参数时不要使用子账户！此外，腾讯云账户需要实名认证。


2. 在这里新建一个访问密钥新建密钥


将SecretId和SecretKey分别配置在仓库的secrets变量里面， TENCENT_SECRET_ID对应你的SecretId的值，TENCENT_SECRET_KEY对应你的SecretKey的值


3. 配置自己需要secrets变量参考这里


重要的说三遍


如果涉及一个变量配置多个值，如多个cookie，多个取消订阅关键字，去掉里面的 空格 和 换行 使用 & 连接

如果涉及一个变量配置多个值，如多个cookie，多个取消订阅关键字，去掉里面的 空格 和 换行 使用 & 连接

如果涉及一个变量配置多个值，如多个cookie，多个取消订阅关键字，去掉里面的 空格 和 换行 使用 & 连接

排查问题第一步先看自己腾讯云函数那边的环境变量跟自己在仓库配置的 secrets 是否一致



4.执行action workflow进行部署，workflow未报错即部署成功


5. 查看和测试
登录后，在 腾讯云函数地址 点击管理控制台，查看最新部署的函数。
在左侧栏的日志查询中，可以查看到触发的日志，包括是否打卡成功等。


6. 设置触发器看这里 或者看这里的注释说明
