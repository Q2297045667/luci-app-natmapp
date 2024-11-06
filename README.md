# luci-app-natmap
全锥NAT的TCP/UDP端口映射

> [NATMap][] 该项目用于建立从ISP NAT公共地址到本地私有地址的TCP/UDP端口映射。如果NAT的所有层都是全锥（NAT-1），则任何主机都可以通过映射的公共地址访问内部服务。

## NATMap之外的功能
- [x] NAT类型测试
- [x] 自动配置防火墙
- [x] 透明端口转发（转发端口=0）
- [x] 刷新BT客户端的侦听端口（转发端口=0）
- [x] 端口更新通知脚本
- [x] 记录更新脚本
- [x] AAAA记录更新脚本
- [x] SRV记录更新脚本
- [x] HTTPS记录更新脚本
- [ ] SVCB记录更新脚本
- [ ] 整合部分[luci-app-natmap](https://github.com/blueberry-pie-11/luci-app-natmap)代码

## 屏幕截图

![0](.img/0.png "0")  

## 依赖

1. [natmapt][]
2. coreutils-timeout
3. [stuntman-client][]

## How to install

1. Go to [here](https://fantastic-packages.github.io/packages/)
2. Download the latest version of ipk
3. Login router and goto **System --> Software**
4. Upload and install ipk
5. Reboot if the app is not automatically added in page
6. Goto **Network --> NATMap**

## Build

Compile from OpenWrt/LEDE SDK

```
# Take the x86_64 platform as an example
tar xjf openwrt-sdk-21.02.3-x86-64_gcc-8.4.0_musl.Linux-x86_64.tar.xz
# Go to the SDK root dir
cd OpenWrt-sdk-*-x86_64_*
# First run to generate a .config file
make menuconfig
./scripts/feeds update -a
./scripts/feeds install -a
# Get Makefile
git clone --depth 1 --branch master --single-branch --no-checkout https://github.com/muink/luci-app-natmapt.git package/luci-app-natmapt
pushd package/luci-app-natmapt
umask 022
git checkout
popd
# Select the package LuCI -> Applications -> luci-app-natmapt
make menuconfig
# Start compiling
make package/luci-app-natmapt/compile V=99
```

## Collaborators

[Richard Yu](https://github.com/ysc3839)  
[Anya Lin](https://github.com/muink)  

[NATMap]: https://github.com/heiher/natmap
[natmapt]: https://github.com/muink/openwrt-natmapt
[stuntman-client]: https://github.com/muink/openwrt-stuntman

## License

This project is licensed under the [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)
