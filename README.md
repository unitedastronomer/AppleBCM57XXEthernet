# AppleBCM57XXEthernet

AppleBCM5701Family.kext from Catalina, patched by **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)**.
  The original thread is in Russian, but someone had made an English explanation [here](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-9#post-1031837).

How to use:
1. Remove existing FakePCIID kexts, Kernel -> Patch entry for AppleBCM5701Family, and device-id spoof under Device Properties.
2. <s>Add your device-id in the kext's Info.plist.</s>

   If you are multi-booting, you could keep FakePCIID kexts by setting its MaxKernel to **19.99.9**, and MinKernel **20.0.0** for AppleBCM577xxEthernet.



Credits: 
- **[Sunki](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-4#post-564218)** for the patching method.
- **[Exception](https://www.applelife.ru/threads/patching-applebcm5701ethernet-kext.27866/page-8#post-930901)** for this modified kext.
- Apple for the AppleBCM5701Family.kext.
