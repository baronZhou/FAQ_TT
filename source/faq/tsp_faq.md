## Trustonic_tee(TSP) FAQ


#### Trustonic TEE、TSP(Trusted Secured Platform)介绍？

> [点击此处-Trustonic Trusted Execution Environment - youtube视频](https://www.youtube.com/watch?v=K7M63z0vCm0)

#### TAP(Trustonic Application Protection)介绍？

> [点击此处-Trustonic Application Protection (TAP) Overview - youtube视频](https://www.youtube.com/watch?v=Zh7jpH96wQ8&t=79s)

#### 如何开启trustonic_tee？

MTK的代码中，已经默认集成了trustonic TEE. 开启Trustonic TEE只需打开下列4个仓库下的宏开关即可

**1、preloader**

(vendor\mediatek\proprietary\bootable\bootloader\preloader\custom\${PROJECT}\${PROJECT}.mk)

```c
MTK_TEE_SUPPORT = yes

TRUSTONIC_TEE_SUPPORT = yes

MICROTRUST_TEE_SUPPORT = no

MTK_GOOGLE_TRUSTY_SUPPORT = no

export MTK_TEE_SUPPORT TRUSTONIC_TEE_SUPPORT MICROTRUST_TEE_SUPPORT MTK_GOOGLE_TRUSTY_SUPPORT
```

**2、kernel**

(${KERNEL_VER}\arch\arm\configs\${PROJECT}_debug_defconfig)<br>
(${KERNEL_VER}\arch\arm\configs\${PROJECT}_defconfig)<br>
(${KERNEL_VER}\arch\arm64\configs\${PROJECT}_debug_defconfig)<br>
(${KERNEL_VER}\arch\arm64\configs\${PROJECT}_defconfig)<br>

```c
CONFIG_TRUSTONIC_TEE_SUPPORT=y

CONFIG_MTK_TEE_GP_SUPPORT=y 
```

**3、projectConfig**

(device\mediatekprojects\${PROJECT}\ProjectConfig.mk)

```c
MTK_ATF_SUPPORT=yes

MTK_TEE_SUPPORT=yes

TRUSTONIC_TEE_SUPPORT=yes

MTK_TEE_GP_SUPPORT=yes 
```

**4、trustzone**

(vendor\mediatek\proprietary\trustzone\custom\build\project\${PROJECT}.mk)

```c
MTK_ATF_SUPPORT=yes

MTK_TEE_SUPPORT=yes

TRUSTONIC_TEE_SUPPORT=yes

MTK_TEE_DRAM_SIZE=0x1740000（根据你自己的TA来调整）

500A
CONFIG_TEE=y 否则无法编译到gud driver
```

#### 如何确认trustonic tee启动OK？

**(1)、通过log确认**

在Kernel log中搜索`Trustonic TEE`关键字，看是否有异常


**(2)、通过log确认**

查看进程是否起来
```c
ps -ef | grep mcDriverDaemon
```

**(3)、通过密码锁**

设置图案锁或密码锁，然后解锁测试


#### MTK平台上使用Trustonic TEE调试指纹的步骤？

- 开启trustonic_tee宏，编译能通过，能开机<br>
- trustonic release internal目录(SDK)给 oem，oem将此目录放入到`vendor/mediatek/proprietary/trustzone/trustonic/`路径下<br>
- oem检查spi驱动的完整性，如不完整，需向MTK申请spi patch<br>
- 在以上步骤完成后，oem编译出spi drv lib库，oem将这些库release给指纹厂商<br>
- 指纹厂商编译出drvlib和talib，release给OEM<br>
- oem将drvlib和talib合入到代码中<br>

#### 如何使用Trustonic TEE SDK编译TA？

#### 如何开启实体RPMB?

MTK代码中，默认使用虚拟RPMB(即persist分区)，如需开启实体RPMB，则需将drRpmb driver打包到tee.img中即可

将drRpmb driver打包到tee.img中有两种方法:
![在这里插入图片描述](pictures/faq_01.png)


#### 如何客制化googlekey？

> [请参考csdn的这篇博客](https://blog.csdn.net/weixin_42135087/article/details/106761192)

#### googlekey安装失败了怎么办？

请确保`test_key.cfg`文件中的`EKKB_PUB`和`PKB`的数组已替换成你们自己的了
```c
(vendor/mediatek/proprietary/trustzone/trustonic/source/bsp/common/500/t-sdk/TlSdk/Out/Bin/KeyReplace/test_key.cfg)

```



