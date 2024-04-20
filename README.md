# AppleBCM57XXEthernet

This is the **AppleBCM5701Ethernet.kext** taken from Catalina, but  patched to work for Big Sur and newer. This kext was originally patched and uploaded by **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** in Apple Life. The original thread is in Russian, but someone had made a well written explanation about it in English [here](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837) ([archived](https://web.archive.org/web/20240407122311/https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)). 



How to use: <br>
1. Add your device-id in the kext's Info.plist if not included. <br>
2. Set MinKernel to **20.0.0**. <br>

#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.AppleBCM57**XX**Ethernet | 35373736 35 | 35373738 36 | 20.0.0 |  | IOReg model 57765 -> 57785 |

Ex. 3 **_5_** 3 **_7_** 3 **_7_** 3 **_6_** 3 **_5_** -> 3 **_5_** 3 **_7_** 3 **_7_** 3 **_8_** 3 **_5_**

# 
<br>
I’m only re-uploading it here because I noticed that the longer the attachment stays in that thread, the more likely it will automatically get deleted.

# 

<br>
<br>

Alternatively, you could also use the [**CatalinaBCM5701Ethernet.kext**](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Ethernet) provided in OCLP repo, and then add these to **Kernel -> Patch**:


|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | E80000FF FF668983 00050000 | B8B41600 00668983 00050000 | 20.0.0 |  | Broadcom BCM577XX Patch |
> This patch is just the same as the `Broadcom BCM57785 Patch` (from the sample.plist of Opencorepkg to load the native kext on Catalina and earlier), but **finds/replace the whole series of hex** without the base and hex masking.

> Even this kext is from Catalina, and in theory the `Broadcom BCM57785 Patch` (from the sample.plist of Opencorepkg) should still be applicable as it was from Catalina anyway, however in my attempt it did not work. Opencore probably does not support masking on injected kexts, hence why I decided to try to find/replace the whole thing instead, and it somehow worked that way.

This is optional. I've had these device properties in my config.plist since the beginning I used this kext, I tried to remove them and the kext still loaded. If that wasn't the case for you, then you may need to add them:


|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|


#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | 35373736 35 | 35373738 36 | 20.0.0 |  | IOReg model 57765 -> 57785 (Cosmetic) |

Ex. 3 **_5_** 3 **_7_** 3 **_7_** 3 **_6_** 3 **_5_** -> 3 **_5_** 3 **_7_** 3 **_7_** 3 **_8_** 3 **_5_**

#
### macOS Catalina and earlier
For Catalina and older, it is possible to use either the: <Br>
1.  The easy way: [FakePCIID and FakePCIID_BCM57XX_as_BCM57765.kext](https://github.com/RehabMan/OS-X-Fake-PCI-ID), or;
2.  The technical way: using the `Broadcom BCM57785 patch` from the sample.plist of Opencorepkg - in combination with device-id, and compatible device property injection of a native model (BCM57765):

|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|

> Don't mind the naming of the patch in the sample.plist. It is named "Broadcom BCM57785 patch" because it was originally made for BCM57785, but it should still work with other model supported by the native kext (via spoofing).

#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report.
|Identifier*|Find|Replace|minKernel|maxKernel| Comment |
|-|-|-|-|-|-|
|com.apple.iokit.AppleBCM5701Ethernet | 35373736 35 | 35373738 36 |  | 19.99.9 | IOReg model 57765 -> 57785 (Cosmetic) |

Ex. 3 **_5_** 3 **_7_** 3 **_7_** 3 **_6_** 3 **_5_** -> 3 **_5_** 3 **_7_** 3 **_7_** 3 **_8_** 3 **_5_**
#

> If you use any of the following that requires device properties injection, the device-id  will show as the spoofed one (14e4,16b4/BCM577**65**) - as these methods require spoofing the ethernet into a native model to make the kext load.

Credits: 
- **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for this patched kext
- **[Andrey1970AppleLife](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)** for Cosmetic patch
- Dortania for CatalinaBCM5701Ethernet
- Acidanthera for the Kernel Patches

