# Thinkpad-L14-Tweaks-Linux (mostly apply to other AMD models of Zen 2/2+, Thinkpads after 2020~ era) Tested on Linux Mint

# TLP aggressive power-saving battery and balanced AC config for L14 AMD Gen 1

Caution: ASPM should not be set to powersupersave for realtek wifi connection stability as per ArchWiki and from personal testing

"The RTW89 kernel module has been merged into the upstream kernel and provides support for newer Realtek wireless chipsets.

This driver supports: 8852AE, 8851BE, 8852BE, and 8852CE.

On some computers, you may experience unstable connections. It seems like a common issue on late models from HP and Lenovo. Try disabling ASPM-related features using the config below. "

Source: https://wiki.archlinux.org/title/Network_configuration/Wireless#Realtek

# Kernel parameters for keyboard quirks and amd suspend issue: 

"atkbd.reset" for keyboard key auto-repeat error and "amdgpu.mcbp=0" for no blank display on resume from lockscreen/ S3 suspend

S3 / [deep] sleep should be chosen for this model, S0ix does not work!!! So far 1.34 bios update does not break S3 / [deep] suspend, but the battery is still 45Wh, so expect around only 5hrs of runtime for a 80% charged battery even already having proper suspend support

# Kernel parameter for low latency:

"preempt=full" (must only be applied after applying "amdgpu.mcbp=0", else freezes on resume happen). Improves desktop experience at the sacrifice of bandwidth
Usecases: https://discourse.ubuntu.com/t/fine-tuning-the-ubuntu-24-04-kernel-for-low-latency-throughput-and-power-efficiency/44834

# Uefi update available via fwupdmgr from LVFS

# Disk tweaks
disk: scheduler set to 'none' for NVME for better performance and less cpu overhead to save battery via tlp (Phoronix benchmark shows none has best first-place finishes)

/tmp relocated to tmpfs for less i/o on ssd for better and better performance (do this you have more than enough ram) Consult Archwiki/ Easy Linux Tips Project for linux mint/ ubuntu)

In bios, set uma buffer size to larger values for better performance (do this you have more than enough ram, else use 'auto') after testing. The perfect value varies from config to config

set trim ssd daily for heavy users (trim is done automatically every 7 days)

# Improve audio quality, for speakers on L14 to compensate for lack of atmos
1. install JamesDSP, open source dsp
2. enable 2x4x2 FFT Convolution script in Liveprog tab
3. All done to improve surround sound on L14
4. extra: invert response of earphones you like to imitate the sound of them via graphic eq tab for better sound (Thanks to JamesDSP and AutoEQ Project)
