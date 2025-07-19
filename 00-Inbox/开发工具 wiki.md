## node相关：
### npm 
是node官方的包管理器，用于安装和发布包
|命令|作用|
|`npm install <包名>`                安装包（写入 `dependencies`）
|`npm install <包名> -dev`      安装包（写入 `devDependencies`）
|`npm install -g <包名>`          全局安装包
|`npm uninstall <包名>`            卸载本地依赖
|`npm uninstall -g <包名>`      卸载全局依赖
|`npm install`                             根据 `package.json` 安装所有依赖
|`npm update`                               更新项目中所有已安装的包
|`npm view [module] versions` 查看依赖的所有可用版本

### nrm
是node的源管理器，用于切换npm源
|命令|作用|
|`nrm ls`|                                       查看所有已添加的 registry 源，以及当前使用的是哪个
|`nrm current`|                             显示当前正在使用的 registry
|`nrm use <源名>`|                        切换到指定的 registry 源（如：`nrm use taobao`）
|`nrm test`|                                   测试所有源的响应速度

### nvm
是node的版本控制器，用于切换不同版本的node和npm，以应对不同环境的要求。
|命令|说明|
|`nvm ls`                                             查看已安装的 Node 版本
|`nvm ls-remote`                               查看可安装的远程 Node 版本
|`nvm install <version>`               安装指定版本 Node
|`nvm use <version>`                       使用指定版本（仅当前终端会话）
|`nvm alias default <version>`   设置默认 Node 版本（每次终端启动时使用）
|`nvm uninstall <version>`           卸载指定版本
|`nvm current`                                   显示当前使用的版本
