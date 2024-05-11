# AppleBCM57XXEthernet
This is the **AppleBCM5701Ethernet.kext** taken from Catalina, patched to work for Big Sur and newer.
* This kext was patched and uploaded by **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** in Apple Life. The original thread is in Russian, but someone had made a well written explanation about it in English [here](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837) ([archived](https://web.archive.org/web/20240407122311/https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)). 

Download the kext [here](https://github.com/unitedastronomer/AppleBCM57XXEthernet/releases/tag/Kext1). Note that this will only work if your specific ethernet model worked with FakePCIID in Catalina.

#### How to use: 
1. Add your device-id in the kext's Info.plist if not included. <br>
2. Set MinKernel to **20.0.0**. <br>

#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report, edit accordingly to match your model.
|Identifier*|Find|Replace|maxKernel| Comment |
|-|-|-|-|-|
|com.apple.iokit.AppleBCM57**XX**Ethernet | 35373736 35 | 35373738 35 | 20.0.0 | IOReg model 57765 -> 57785 |

3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**6**</kbd> 3 <kbd>**5**</kbd> -> 3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**8**</kbd> 3 <kbd>**5**</kbd>

# 
<br>
I’m only re-uploading it here because I noticed that the longer the attachment stays in that thread, the more likely it will automatically get deleted.

# CatalinaBCM5701Ethernet
Alternatively, you could also use the [**CatalinaBCM5701Ethernet.kext**](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Ethernet) provided in OCLP.

Add these to **Kernel -> Patch** AS IT IS:
|Identifier*|Find|Replace|minKernel| Comment |
|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | E8CA9EFF FF668983 00050000 | B8B41600 00668983 00050000 | 20.0.0 | Broadcom BCM577XX Patch |

Add these device properties. Do not inject your real device-id, we will to spoof it to a natively supported one, copy the following as it is:  

|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|

Or you could try adding your device-id inside the info.plist instead, but I have not tested it.

#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report, edit accordingly to match your model.
|Identifier*|Find|Replace|minKernel| Comment |
|-|-|-|-|-|
|com.apple.iokit.CatalinaBCM5701Ethernet | 35373736 35 | 35373738 35 | 20.0.0 | IOReg model 57765 -> 57785 (Cosmetic) |

3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**6**</kbd> 3 <kbd>**5**</kbd> -> 3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**8**</kbd> 3 <kbd>**5**</kbd>

#
### macOS Catalina and earlier
For Catalina and older, it is possible to use either the: <Br>
1.  The easy way: [FakePCIID and FakePCIID_BCM57XX_as_BCM57765.kext](https://github.com/RehabMan/OS-X-Fake-PCI-ID), or;
2.  Using the `Broadcom BCM57785 Patch` from the sample.plist of Opencorepkg - in combination with `device-id`, and `compatible` device property injection of a native model (BCM57765). Do not inject your real device-id, we will need to spoof it to a natively supported one, copy the following as it is:
    
|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|

#### Cosmetic
This is optional. You could also apply a **Kernel -> Patch** to show the correct model in System Report, edit accordingly to match your model.
|Identifier*|Find|Replace|maxKernel| Comment |
|-|-|-|-|-|
|com.apple.iokit.AppleBCM5701Ethernet | 35373736 35 | 35373738 36 | 19.99.9 | IOReg model 57765 -> 57785 (Cosmetic) |

3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**6**</kbd> 3 <kbd>**5**</kbd> -> 3 <kbd>5</kbd> 3 <kbd>7</kbd> 3 <kbd>7</kbd> 3 <kbd>**8**</kbd> 3 <kbd>**5**</kbd>

If you use any of the method that needed device properties injection, the device-id  will show as the spoofed one (14e4,16b4/BCM577**65**).

Credits: 
- **[Sunki](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for coming up with the patches - that was used for the `AppleBCM57XXEthernet`
- **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for this patched kext
- **[Andrey1970AppleLife](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837)** for Cosmetic patch
- Dortania for CatalinaBCM5701Ethernet
- Acidanthera/Sunki for the Kernel Patches
