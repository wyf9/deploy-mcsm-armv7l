# deploy-mcsm-libs

在一些冷门系统上部署 MCSManager 用到的依赖

## 如何使用

### 错误提示

如果你安装 MCSManager Daemon，在启动时遇到下面的错误：

```
root@onecloud:/opt/mcsmanager/daemon# /opt/node-v16.20.2-linux-armv7l/bin/node app.js
[09/16 18:24:42] [INFO] All feature modules and permission firewalls have been initialized successfully

______  _______________________  ___                                         
___   |/  /_  ____/_  ___/__   |/  /_____ _____________ _______ _____________
__  /|_/ /_  /    _____ \__  /|_/ /_  __ `/_  __ \  __ `/_  __ `/  _ \_  ___/
_  /  / / / /___  ____/ /_  /  / / / /_/ /_  / / / /_/ /_  /_/ //  __/  /    
/_/  /_/  \____/  /____/ /_/  /_/  \__,_/ /_/ /_/\__,_/ _\__, / \___//_/     
                                                        /____/               
________                                                                     
___  __ \_____ ____________ ________________                                 
__  / / /  __ `/  _ \_  __ `__ \  __ \_  __ \                                
_  /_/ // /_/ //  __/  / / / / / /_/ /  / / /                                
/_____/ \__,_/ \___//_/ /_/ /_/\____//_/ /_/                                 
                                                                             

 + Copyright 2024 MCSManager Dev <https://github.com/MCSManager>
 + Version 4.4.1

/opt/mcsmanager/daemon/app.js:5235
            throw new Error((0, i18next_1.t)("TXT_CODE_6915f2a") + path);
            ^

Error: Dependency files are missing and cannot be started. Please reinstall the program:/opt/mcsmanager/daemon/lib/pty_linux_arm
    at /opt/mcsmanager/daemon/app.js:5235:19
    at Array.forEach (<anonymous>)
    at checkDependencies (/opt/mcsmanager/daemon/app.js:5233:18)
    at Object../src/app.ts (/opt/mcsmanager/daemon/app.js:870:38)
    at __webpack_require__ (/opt/mcsmanager/daemon/app.js:7425:42)
    at /opt/mcsmanager/daemon/app.js:7436:37
    at Object.<anonymous> (/opt/mcsmanager/daemon/app.js:7438:12)
    at Module._compile (node:internal/modules/cjs/loader:1198:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1252:10)
    at Module.load (node:internal/modules/cjs/loader:1076:32)
```

如你所见，其中提示缺失文件: `/opt/mcsmanager/daemon/lib/pty_linux_arm`

### 获取 lib

拆分这个路径：

- `/opt/mcsmanager/daemon/lib/` - 你的 lib 目录
- `pty` - lib 名称
- `linux_arm` - 架构

#### 直接下载构建好的库文件

查找 `本 repo` -> `dist` -> 你的架构

如果找到，复制里面的两个文件到你的 lib 目录:

- `file_zip_你的架构`
- `pty_你的架构`

再次启动 MCSM 即可.

#### 手动构建

如果没有你的版本，可以选择手动构建:

1. 获取源代码

进入本仓库的子模块 `pty-src`, `zip-tools-src` 并切换到主分支 (或在 `你的 libs 目录` -> `source-code.txt` 查找两个 repo)

在目标机器上 clone repo，或直接下载仓库源码 / Release:

```shell
git clone https://github.com/MCSManager/PTY.git
```

```shell
git clone https://github.com/MCSManager/Zip-Tools.git
```

2. 编译

首先确认你已经安装了 Go > `1.21` *(最好是最新版本?)*

然后依次进入两个仓库的根目录，并执行 `go build` 以编译:

```shell
# export http_proxy=你的代理地址; export https_proxy=你的代理地址
cd PTY
go build
cd ../Zip-Tools
go build
cd ..
```

> 大陆机器可能需要设置环境变量 `http_proxy`, `https_proxy` 来指定代理下载

3. 放置 lib 文件

重命名产物:

- PTY (`pty`) -> `pty_你的架构`
- Zip-Tools (`file-zip`) -> `file_zip_你的架构`

将它们放入你的 lib 目录，再次启动 MCSM 即可.