## 安装`John`(为了提取`hash`)
```
wget https://github.com/sanbei101/crack/releases/download/crack/john.zip
unzip -q john.zip
```

## 测试
```
zip -r -P  123456pwd test.zip .github

./john/run/zip2john test.zip > raw_hash.txt
```

## 提取为`HashCat`可识别的格式
```
awk -F: '{print $2}' raw_hash.txt > hash.txt
```

## 安装`HashCat`
```
wget https://github.com/sanbei101/crack/releases/download/crack/hashcat.zip
unzip -q hashcat.zip
```

## 使用`HashCat`

### 穷举模式
```
./hashcat/hashcat.bin -m 17200 -a 3 -w 4 \
  -i --increment-min 4 --increment-max 9 \
  hash.txt '?a?a?a?a?a?a?a?a?a'
```

### 密码字典模式
```
wget https://github.com/sanbei101/crack/releases/download/crack/rockyou.txt
```

```
./hashcat/hashcat.bin -m 17200 -a 0 -w 4 \
  -r ./hashcat/rules/best66.rule \
  hash.txt rockyou.txt
```
