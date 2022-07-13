# frida_api_server
- 使用 flask_restful 写的 frida rpc 服务
- 可以连接多台手机，可以同时 hook 多个 app
- 每个 app 只会 attach 一次，这样可以减少内存消耗，以免 app 挂掉
- 每次 hook 前都会都会检测，当前 attach 的对象是否存在，不存在则重新 attach
- 代码里有加，自动重启，目标 app，frida-server（经过测试，android 7.x 以上没问题，6.x frida-server 会启动失败）

# 使用
##### 运行 `run.py` 启动服务，默认监听 `6999` 端口（config.py 文件里修改）

## frida rpc
在 `frida_hook` 文件夹下编写，例如某手，已有样例

### 详情请阅读代码
    1. 安装的frida版本一定要对应
    2. 安装frida 这里已夜神为例 
    http://91fans.com.cn/post/emuxposedfrida/#gsc.tab=0
    夜神Frida
    先adb连上夜神，看看它是嘛系统
    fenfeiMac:Desktop ff$ adb connect 127.0.0.1:62001
    already connected to 127.0.0.1:62001
    fenfeiMac:Desktop ff$ adb shell getprop ro.product.cpu.abi
    x86
    把对应的 fridaServer拷进去
    adb push frida-server-15.1.24-android-x86 /data/local/tmp/frida-server
    跑起来
    adb shell
    su
    cd /data/local/tmp
    chmod 755 frida-server
    ./frida-server
    
    3. 算法
    sig getSign
    sig3 getNSSign3
    tokensig sha256 sig+salt
