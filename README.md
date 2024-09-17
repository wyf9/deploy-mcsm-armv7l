# deploy-mcsm-libs

在一些冷门系统上部署 MCSManager 用到的依赖

## 如何使用

如果你安装 MCSManager Daemon，在启动时遇到下面的错误：

```
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