> my gpg key ID：luoaijun
## GPG 基本指令

###### 查看gpg版本

```
gpg --version
```


###### 生成gpg key

```
gpg --gen-key
```

###### 请求撤销gpg key

```
gpg --ken-revoke
```


###### 列出gpg key

```
gpg --list-keys
```

 
###### 上传gpg key到公共服务器

```
gpg --keyserver [keyservers.address.com] --send-keys  [your pubID] 
```
- 例子：

```
gpg --keyserver hkp://subkeys.pgp.net  --send-keys  EBBADF510F5DAF7B377D24E51669F1F4C0A979ED
```


###### 加密文件
1. Function
```
gpg -o encrypted_file.gpg --encrypt -r key-id original.file
```


```
（1）-o encrypted_file.gpg = 指定输出文件
（2）--encrypt = 做加密
（3）-r = 接收者的KEY-ID，比如这里就填你朋友的KEY-ID。
（4）original.file = 指定要加密的文件
```

2. Function
```
gpg --recipient [your pubID]--output out.file  --encrypt original.file
```

###### 查找gpg key

```
gpg --search-keys  [用户ID]
```
###### 加密文件

- 搜索对方的公钥。
```
gpg --list-key aijun.luo@outlook.com
```
- 利用对方的公钥加密：

```
 gpg --recipient [公钥ID] --output text.txt --encrypt text
```
- 对方利用自己的公钥对应的私钥解密：

```
gpg --decrypt filename.gpg
```

###### 删除公钥
```
gpg --delete-secret-keys [公钥ID]
```
###### 签名
```
gpg --clearsign text.txt
gpg --sign text.txt
```

###### 验证文件完整性 
```
gpg --verify text.txt.asc
```
