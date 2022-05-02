# Windows 10

## 重装系统后

### 驱动

- [acer 产品支持-驱动程序和使用手册](https://www.acer.com.cn/service-support.html?ImageURL=Image/ModelPictures/Ultra-thin/SF314-54.png&name=SF314-54&type=1&ProductLine=Swift&ProductFamily=%25E8%25B6%2585%25E8%25BD%25BB%25E8%2596%2584)
  - 找不到支持 Windows hello 指纹的指纹识别器 (Install drivers using Device Manager, show hidden devices, ..., then reboot; [check](https://answers.microsoft.com/zh-hans/windows/forum/all/win-10-%E6%98%BE%E7%A4%BA/03b65683-02f8-4f88-acf1-60945414a2b5) (p.s. 22/01/13 的解决则是：在以管理员身份运行的 cmd 中，运行对应的驱动中的 .bat 文件)
  - no OSD? just install the Acer Quick Access [also check](https://community.acer.com/en/discussion/465699/disable-caps-lock-notification-on-screen)
- [asus rog 14 related](https://rog.asus.com.cn/laptops/rog-zephyrus/rog-zephyrus-g14-series/HelpDesk_Download)

### customization

[the latest clash](https://github.com/Fndroid/clash_for_windows_pkg/releases)

to [disable internet search](https://superuser.com/questions/1196618/how-to-disable-internet-search-results-in-start-menu-post-creators-update#), run the following commands in Powershell

```
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v BingSearchEnabled /t REG_DWORD /d 0
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v AllowSearchToUseLocation /t REG_DWORD /d 0
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v CortanaConsent /t REG_DWORD /d 0
```

[禁用时间轴](https://blog.csdn.net/cumai3211/article/details/109041476) Settings - Privacy - Activity history - toggle the `在此设备上存储 xxx`

[do not show recently added section at the top of start menu app list](https://www.howtogeek.com/694731/how-to-remove-recently-added-apps-in-windows-10s-start-menu/) Settings - Personalization - Start - toggle the `show recent added apps` button

[create a system restore point before doing any registry modifications](https://www.youtube.com/watch?v=9IU6Y7IW00o) 高级系统设置 - 系统保护 tab

[桌面上无 Desktop icon?](https://www.online-tech-tips.com/computer-tips/desktop-icons-missing-or-disappeared/) Settings - Personalization - Theme - Desktop icon settings

[ie 卸了再装回来](https://www.zhihu.com/question/60218250) 设置 - 应用 - 应用和功能 - 可选功能

登录微软账号错误？[换微软的dns](https://www.zhihu.com/question/39072396/answer/82532105) `4.2.2.1` and `4.2.2.2`

## what is

_烫烫烫_ 乱码最常见的地方是 Visual Studio。VS 中未初始化的栈空间用`0xCC`填充，而未初始化的堆空间用`0xCD`填充。而`0xCCCC`和`0xCDCD`在中文GB2312编码中分别对应"烫"字和"屯"字。[source](https://www.zhihu.com/question/36899383/answer/69503032)

`msdia80.dll` file directly on the other hard drive? [This file is normally installed by Microsoft Visual C++. The correct path should be **C:\Program Files (x86)\Common Files\microsoft shared\VC**.](https://www.sevenforums.com/general-discussion/334580-msdia80-dll-directly-my-other-hard-drive-post2802903.html#post2802903) If u can confirm that file exists in the correct path as well, u could safely delete the file on that drive. Otherwise, move the file to the correct path and register it: run cmd as administrator and `regsvr32 C:\Program Files (x86)\Common Files\microsoft shared\VC\msdia80.dll`.

_Xbox Game Bar_ the resolution is 1080p on most systems, high framerates; it is meant to be a source material [check](https://www.quora.com/Why-does-videos-recorded-by-Windows-10-Win-key-+-G-take-up-so-much-space-Its-like-a-10-mins-video-almost-takes-up-an-entire-GB)

## how to

activate **GodMode**(a special folder that gives you quick access to over 200 tools and settings that are normally tucked away in the Control Panel and other windows and menus): create a folder, then rename it with `God Mode.{ED7BA470-8E54-465E-825C-99712043E01C}` [source](https://www.lifewire.com/god-mode-windows-4154662)

连接 Bose QC35 II ? **make your laptop discoverable via Bluetooth**

[get the environment variables?](https://superuser.com/questions/341192/how-can-i-display-the-contents-of-an-environment-variable-from-the-command-promp)
- with Command-Prompt, use `echo %PATH%` to get one env var; use `set` to get all stuff
- with Powershell, use `echo $env:PATH` to get one; use `ls env:` for listing all

[remove `git bash here` in contextual menu?](https://stackoverflow.com/questions/47084443/how-to-remove-git-from-menu-context-in-documents) check the following places 
- `HKEY_CLASSES_ROOT\LibraryFolder\background\shell`
- `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\background\shell`
- `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\shell\git_shell`

[run java apps unscaled on a high dpi display?](https://superuser.com/a/1207925/1233932) find `java.exe` you installed > Properties > Compatibility > check `Override high DPI scaling behavior` > choose `System` for `Scaling performed by`.

[show connected Wi-Fi password](https://support.microsoft.com/en-us/windows/find-your-wi-fi-network-password-in-windows-2ec74b2e-d9ec-ade1-cc9b-bef1429cb678#:~:text=In%20Network%20and%20Sharing%20Center,the%20Network%20security%20key%20box)
1. Settings > Network & Internet > Status > Network and Sharing Center.
2. In Network and Sharing Center, next to **Connections**, select your Wi-Fi network name.
3. In Wi-Fi Status, select **Wireless Properties**.
4. In Wireless Network Properties, select the **Security** tab, then select the **Show characters** check box. Your Wi-Fi network password is displayed in the Network security key box.

[Turn off antivirus protection in Windows Security](https://support.microsoft.com/en-us/windows/turn-off-antivirus-protection-in-windows-security-99e6004f-c54c-8509-773c-a4d776b77960) **Virus & threat protection** > **Manage settings**, then switch **Real-time protection** to **Off**.

[change windows console font family](https://superuser.com/questions/5035/how-to-change-the-windows-xp-console-font), not recommend, however, make sure to save a system restore point if before u do that.

[关闭笔记本自带键盘 - 知乎harry159821的回答](https://www.zhihu.com/question/36434420/answer/279030735)

[Windows 无法弹出U盘终极解决方法](https://zhuanlan.zhihu.com/p/161364971) 管理工具 - 事件查看器 - 管理事件 - 等等等等

[remove items from the right click context menu](https://superuser.com/questions/5011/how-to-remove-items-from-the-right-click-context-menu-in-windows)

[电脑设置了不锁屏，但是过几十分钟还会自动熄屏](https://stackoverflow.com/a/20256087/11844003) 用脚本模拟鼠标移动 (what about PowerToy? YES)

["open with" not appearing as an option](https://superuser.com/questions/841497/windows-open-with-application-not-appearing-as-an-option)

1. open command prompt as admin
2. check `assoc .your_f_type`, e.g.
   - `assoc .class` -> xxx not found xxx ? associate it, `assoc .class=javaclass` : good to go
3. `ftype {f_assoc}` the `f_assoc` is the output of the last command (or the one you decided), e.g.
   - `ftype javaclass` -> xxx no xxx ? make it, `ftype javaclass="path\to\jd-gui.exe" "%1"` : good to go
   - note, `ftype` with no parameters will display all file types and the executable program for each

## why

错误信息：`C:\Program` 不是不是内部或外部命令 也不是可运行的程序？这是因为 Java 安装在了 `C:\Program Files\` 下 导致最终的 PATH 变量中包含了空格

在删除文件时电脑提示需要权限，在更改权限后显示拒绝访问, [你大概率是打开了文件夹里的某个文件，导致他正在运行你无法删除](https://www.zhihu.com/question/396012845/answer/1234094326)

在线语音自己讲话没声音? 查看设置中 "是否允许应用访问你的麦克风"

[把一个大文件移入到另一个u盘或硬盘里，提示对于目标文件系统过大无法移动，就是该盘的文件系统导致的，转换为 NTFS 即可](https://blog.csdn.net/qq_42249896/article/details/89017833) `convert your-drive-letter:/fs:ntfs`

[win10资源管理器占用CPU过高](https://www.zhihu.com/question/39000100) 本人的情况应该是带有 QTTabBar 的 Explorer 开了很多 tab 并且文件层次深？

[突然不显示日期和星期了](https://www.zhihu.com/question/20521579) 任务栏是垂直放置，是宽度问题导致的，可以尝试拉宽任务栏，或者 设置 - 时间和语言 - 日期和时间 - 右侧相关设置的日期时间和区域格式设置 - 更改数据格式 - 把短日期格式改一下（改完之后 Explorer 里显示的修改时间也变了哦）

When transferring data, if you move one large file, you only have to write the directory entry once and then stream the data and write more or less continuously. When you have many files, you write the directory info, move to the file area and write the data, then go back and write the directory entry for the next file and then move back to the data area and write the data and back and forth. The overhead of moving back and forth adds up. [[Source](https://superuser.com/a/857248/1233932)]

When a file is written to a file system, it may consume slightly more [disk space](https://en.wikipedia.org/wiki/Disk_space) than the file requires. This is because the file system rounds the size up to include any unused space left over in the last [disk sector](https://en.wikipedia.org/wiki/Disk_sector) used by the file. (A _sector_ is the smallest amount of space addressable by the file system. The size of a disk sectors is several hundred or several thousands bytes.) The wasted space is called **slack space** or **internal fragmentation**. Although smaller sector sizes allow for denser use of disk space, they decrease the operational efficiency of the file system.

touch-pad lagging movement - 断电之后触摸板好使了，插上电后又恢复迟钝的状态，可能是那个插座 **电工偷工减料220v火线没有接地线导致有弱点干扰了笔记本电容触屏控** [出处](https://www.bilibili.com/read/cv6924005)

### wtf

[微软拼音输入法未显示选字栏](https://blog.csdn.net/Reborn_Lee/article/details/107445793) 微软拼音 -> 常规 -> 兼容性 -> 选择以前版本的输入法

taskbar icon highlight sticks [check this](https://superuser.com/questions/61833/windows-7-taskbar-icon-highlight-sticks) and [this](https://www.reddit.com/r/Windows10/comments/4qlgqp/taskbar_icons_stay_highlighted_orange_forever/), u can try resetting the system

**snip & sketch** [flickering screen](https://answers.microsoft.com/en-us/windows/forum/all/screen-flickering-while-using-snip-and-sketch/6311d87d-d356-469e-a809-4cea7a67eddf), do the **reset** stuff

`dwm.exe` high memory usage (just kill the process or service, it'll restart and back to normal state)

git bash chinese garbled [try this one?](https://gist.github.com/nightire/5069597), (ok if windows cmd, or with git open in WT) [参考](https://github.com/microsoft/terminal/issues/1294#issuecomment-502539208)

[partial keyboard not working](https://answers.microsoft.com/en-us/windows/forum/windows_10-other_settings-winpc/standard-ps2-keyboard-is-not-working/4d7f0de2-bf00-4cfb-bddb-5e34fc8604fa); [try with method 4](http://troubleshooter.xyz/wiki/keyboard-has-stopped-working-on-windows-10/)

[ctrl+空格这个热键只在微软拼音下生效](https://www.zhihu.com/question/36005148)

鼠标左键双击打开了属性窗口 - alt 键卡了?

windows [reduce osd time out](https://superuser.com/questions/1006965/how-to-reduce-osd-time-out), 5s is the minimum value

## todo

- [ ] your privacy (sandbox?)
- [ ] [需要来自 Trustedinstaller 的权限](https://zhuanlan.zhihu.com/p/108569823)
- [ ] [remove windows built-in items from right-click context menu](https://superuser.com/questions/742727/remove-windows-built-in-items-from-right-click-context-menu)
- [ ] [磁盘分区](https://zhuanlan.zhihu.com/p/52141844)
- [ ] `dwm.exe` high cpu usage
- [ ] 22/1/29 io error (外接固态盘，部分目录打开就提示，有些是查看文件内容提示)
- [ ] 22/3/26 process suspended
