# exhausted-robot

- [救砖](http://bbs.gfan.com/android-8433589-1-1.html)

- [how to](https://www.itfanr.cc/2018/10/16/google-pixel-unlock-bl-and-root/) root

  ```bash
  adb reboot bootloader
  fastboot boot xxx.img
  ```

- [hack VoLTE](https://cloud-atlas.readthedocs.io/zh_CN/latest/android/hack/pixel_volte.html)

- [?](http://bbs.gfan.com/android-9623353-1-1.html)

  1. adb devices
  2. adb shell
  3. su
  4. setenforce 0
  5. setprop sys.usb.configfs 1 && setprop sys.usb.config diag,serial_cdev,rmnet_gsi,adb

- [copy files using adb to android](https://stackoverflow.com/questions/39441477/how-to-copy-file-using-adb-to-android-directory-accessible-from-pc)

  ```bash
  adb push somefile /sdcard/somewhere
  ```

- [show device properties using adb](https://stackoverflow.com/questions/21099301/android-adb-commands-to-get-the-device-properties), e.g.,  get a general info

  ```bash
  adb shell getprop
  ```

- 刚恢复出厂设置的 pixel xl 能连上 wifi 但"网络连接受限"? 把一张有上网功能的 sim 卡插入再拔出后就能连网啦
