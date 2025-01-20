# Thinkpad-L14-Tweaks-Linux (mostly apply to other AMD models of Zen 2/2+, Thinkpads after 2020~ era) Tested on Linux Mint

# TLP aggressive power-saving battery and balanced AC config for L14 AMD Gen 1

Caution: ASPM should not be set to powersupersave for realtek wifi connection stability as per ArchWiki and from personal testing

"The RTW89 kernel module has been merged into the upstream kernel and provides support for newer Realtek wireless chipsets.

This driver supports: 8852AE, 8851BE, 8852BE, and 8852CE.

On some computers, you may experience unstable connections. It seems like a common issue on late models from HP and Lenovo. Try disabling ASPM-related features using the config below. "

Source: https://wiki.archlinux.org/title/Network_configuration/Wireless#Realtek

# Kernel parameters for keyboard quirks and amd suspend issues: 

"atkbd.reset" for keyboard key auto-repeat error

S3 / [deep] sleep should be chosen for this model, S0ix does not work!!! So far 1.34 bios update does not break S3 / [deep] suspend, but the battery is still 45Wh, so expect around only 5hrs of runtime for a 80% charged battery even already having proper suspend support

# Parameters for low latency:

"preempt=full". Improves desktop experience at the sacrifice of bandwidth
Usecases: https://discourse.ubuntu.com/t/fine-tuning-the-ubuntu-24-04-kernel-for-low-latency-throughput-and-power-efficiency/44834

net.core.default_qdisc = fq_pie in /etc/sysctl.conf for better low latency experience( tested on my AMD machine with 8852AE chip)
(remember to load kernel module sch_fq_pie before setting)


w /proc/sys/vm/page_lock_unfairness - - - - 1
w /proc/sys/vm/page-cluster - - - - 0
w /proc/sys/vm/watermark_boost_factor - - - - 0

setting in /etc/tmpfiles.d/xxxx.conf (xxxx= any name) will lower maximum latency while maintaining decent throughput and consistency for gaming

# Uefi update available via fwupdmgr from LVFS

# Disk tweaks
disk: scheduler set to 'none' for NVME for better performance and less cpu overhead to save battery via tlp (Phoronix benchmark shows none has best first-place finishes)

/tmp relocated to tmpfs for less i/o on ssd for better performance (do this you have more than enough ram) Consult Archwiki/ Easy Linux Tips Project)

In bios, set uma buffer size to larger values for better performance (do this you have more than enough ram, else use 'auto') after testing. The perfect value varies from config to config

set trim ssd daily for heavy users (trim is done automatically every 7 days)
