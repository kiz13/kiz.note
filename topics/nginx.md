# nginx

[beginner's guide](https://nginx.org/en/docs/beginners_guide.html)

start nginx: `start nginx.exe`

By default, the configuration file is named `nginx.conf`

once nginx is started, it can be controlled by invoking the executable with the `-s` parameter:

```shell
nginx -s some_signal
```

that signal may be one of the following:

- `stop` fast shutdown
- `quit` graceful shutdown
- `reload` reloading the configuration file
- `reopen` reopening the log files

for getting the list of all running nginx processes

```shell
tasklist /fi "imagename eq nginx.exe"
```

---

知乎 - [8分钟深入浅出](https://zhuanlan.zhihu.com/p/34943332)

[nginx multiple location issues](https://serverfault.com/questions/361159/nginx-multiple-location-issues)

[what is the `location`](https://serverfault.com/questions/674425/what-does-location-mean-in-an-nginx-location-block)

[meaning of the tilde sign \(`~`\) in the location block](https://serverfault.com/questions/581474/nginx-meaning-of-the-tilde-in-the-location-block-of-the-nginx-conf)

[location directive not working?](https://serverfault.com/questions/596618/location-directive-not-working)

[configure nginx response mime-type?](http://www.nginxer.com/records/how-to-configure-nginx-to-return-text-or-json)

[what does `^` and `$` stand for](https://stackoverflow.com/questions/26016677/what-does-the-two-symbols-and-stand-for-in-nginx-configuration)

[using regex in the location settings block section](https://stackoverflow.com/questions/59846238/guide-on-how-to-use-regex-in-nginx-location-block-section)
