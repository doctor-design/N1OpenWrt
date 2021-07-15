
N1打包学习测试，请不要使用。

# 如何使用
1. fork项目
2. 在secrets中创建RELEASES_TOKEN，一般一次编译要2~4小时，所以要创建一个github发布用的token。
3. 点击Actions -> Workflows -> Run workflow -> Run workflow 
4. N1 Multiple Version 多版本编译
5. N1 Single Version 只编译一个版本
6. Update Checker, 上游更新则编译。MULTIPLE_BUILD: true **编译mini和plus多版本编译**  false，**只编译mini**


openwrt rootfs 编译注意事项：

       Target System  ->  QEMU ARM Virtual Machine 
       Subtarget ->  QEMU ARMv8 Virtual Machine (cortex-a53)
       Target Profile  ->  Default
       Target Images  ->   tar.gz
       *** 必选软件包(基础依赖包，仅保证打出的包可以写入EMMC,可以在EMMC上在线升级，不包含具体的应用)： 
       Languages -> Perl               
                    ->  perl-http-date
                    ->  perlbase-getopt
                    ->  perlbase-time
                    ->  perlbase-unicode                              
                    ->  perlbase-utf8        
       Utilities -> Disc -> blkid、fdisk、lsblk、parted            
                 -> Filesystem -> attr、btrfs-progs(Build with zstd support)、chattr、dosfstools、
                                  e2fsprogs、f2fs-tools、f2fsck、lsattr、mkf2fs、xfs-fsck、xfs-mkfs    
                 -> Shells  ->  bash         
                 -> gawk、getopt、losetup、tar、uuidgen

        * (可选)Wifi基础包：
        *     打出的包可支持博通SDIO无线模块,Firmware不用选，
        *     因为打包源码中已经包含了来自Armbian的firmware，
        *     会自动覆盖openwrt rootfs中已有的firmware
        Kernel modules  ->   Wireless Drivers -> kmod-brcmfmac(SDIO) 
                                              -> kmod-brcmutil
                                              -> kmod-cfg80211
                                              -> kmod-mac80211
        Network  ->  WirelessAPD -> hostpad-common
                                 -> wpa-cli
                                 -> wpad-basic
                 ->  iw
       
    
    除上述必选项以外的软件包可以按需自主选择。

# 感谢
 * [mingxiaoyu](https://github.com/mingxiaoyu/N1Openwrt)
 * [P3TERX](https://github.com/P3TERX/Actions-OpenWrt)提供的脚本参考
