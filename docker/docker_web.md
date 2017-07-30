# docker web服务访问
* 运行环境  
主机IP：A  
虚拟机IP：B  
虚拟机中访问docker服务的IP：C  
docker服务暴露的端口：D  
虚拟机中映射端口：E  
* 要点  
主机与虚拟机通过桥接方式连接（virtualbox设置路径：设置->网络->网卡1->连接方式）  
虚拟机中访问：C:E  
主机中访问：B:E  
