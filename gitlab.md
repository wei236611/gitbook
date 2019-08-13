## 1、创建ssh key
```bash
ssh-keygen -t rsa -C "your_email@**.com" //邮箱为Gitlab注册邮箱

```
![步骤1](https://pinpai-portal-rs.eebbk.net/pinpai-portal/pic/2019/08/13/1565668097359/1.png)

## 2、打开本地的ssh key文件，默认地址为C:\Users\xx\.ssh，xx代表电脑名称，打开id_rsa.pub，复制里面的key，然后在gitlab网站后台添加SSH Keys