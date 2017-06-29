# Docker 加速

## Docker Toolbox
（不推荐使用 docker toolbox，建议使用新的 docker for mac 及 docker for windows 以在这两种平台运行 docker ）
请确认你的 Docker Toolbox 已经启动，并执行下列命令（请将 加速地址 替换为在加速器页面获取的专属地址）
```
docker-machine ssh default
sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=加速地址 |g" /var/lib/boot2docker/profile
exit
docker-machine restart default
```

* [DaoCloud 加速器地址（需要注册账号）](https://www.daocloud.io/mirror#accelerator-doc)


---
**参考资料**
* [Docker 加速器](http://guide.daocloud.io/dcs/daocloud-9153151.html#docker-toolbox)
* [在Windows中玩转Docker Toolbox](http://www.cnblogs.com/studyzy/p/6113221.html)
