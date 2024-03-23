# AppleBCM57XXEthernet

This is a AppleBCM5701Family.kext taken from Catalina, patched by **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)**. This was taken from an Applelife.ru forum, the original thread is in Russian, but someone had made an English explanation of how it works [here](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837). This will only work if your specific ethernet model worked under Catalina!

How to use:
1. Remove existing FakePCIID kexts.
2. Add your device-id in the kext's Info.plist if not included.
3. Set MinKernel to **20.0.0**.


> [!TIP]
> If you are multi-booting pre-Big Sur, you COULD delete FakePCIID kexts and activate the `Broadcom BCM57785 Patch` in your config.plist, this will also load the native kexts just like what FakePCIID do. If you have deleted it before, copy the `Broadcom BCM57785 Patch` from the default config.plist from OpencorePkg, then add these device properties for your ethernet:

|Key*|Value|Type|
|-|-|-|
|compatible |pci14e4,16b4 |String |
|device-id|B4160000|Data|
|built-in|01|Data|


#### Cosmetic / Optional
If you are using the patch and device property injection, it will show a model name of `57765` in system report - this is because of device-id spoofing. If you don't like that, just keep using FakePCIID kexts instead of doing the kernel -> patch and device properties injection.

Credits: 
- **[Sunki](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-4#post-564218)** for the patching method.
- **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for this patched kext.
- Apple for the AppleBCM5701Family.kext.
