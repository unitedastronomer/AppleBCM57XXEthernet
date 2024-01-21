# AppleBCM57XXEthernet

This is a patched kext taken from Catalina for enabling Broadcom ethernet under Big Sur and newer. This was taken from a thread in Apple Life, the original thread is in Russian, but someone had made a really good explanation in English [here](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837) ([archived](https://web.archive.org/web/20240407122311/https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)). This will only work if your specific ethernet model worked under Catalina!



How to use: <br>
1. Add your device-id in the kext's Info.plist if not included. <br>
2. Set MinKernel to **20.0.0**. <br>

#### Cosmetic
You could also apply a Kernel -> Patch to show the correct IOReg model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.AppleBCM57**XX**Ethernet | 35373736 35 | 35373738 36 | 20.0.0 |  | IOReg model 57765 -> 57786 |

Ex. 3 **_5_** 3 **_7_** 3 **_7_** 3 **_6_** 3 **_5_** -> 3 **_5_** 3 **_7_** 3 **_7_** 3 **_8_** 3 **_6_**

I’m only re-uploading it here because I noticed that the longer the attachment stays in that thread, the more likely it is to get automatically  deleted.
# 
<br>
<br>

Alternatively, you could use the **CatalinaBCM5701Ethernet.kext** provided in OCLP repo, and add these to Kernel -> Patch:

|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | E80000FF FF668983 00050000 | B8B41600 00668983 00050000 | 20.0.0 |  | Broadcom BCM577XX Patch |

Add these to device properties:
|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|

#### Cosmetic
You could also apply a Kernel -> Patch to show the correct IOReg model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | 35373736 35 | 35373738 36 | 20.0.0 |  | IOReg model 57765 -> 57786 (Cosmetic) |



#
### macOS Catalina and earlier
For Catalina and older, it is possible to use either the (1) FakePCIID - the easy way, or (2) the technical way - using the BCM57785 Patch from the sample.plist of Opencorepkg - in combination with device-id, and compatible device property injection of a native model (BCM57765):

|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|

#### Cosmetic
You could also apply a Kernel -> Patch to show the correct IOReg model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.AppleBCM5701Ethernet | 35373736 35 | 35373738 36 |  | 19.99.9 | IOReg model 57765 -> 57786 (Cosmetic) |




Credits: 
- **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for this patched kext
- **[Andrey1970AppleLife](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)** for Cosmetic patch
- Dortania for CatalinaBCM5701Ethernet
- Acidanthera for the Kernel Patches

