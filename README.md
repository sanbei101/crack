## 安装`John`(为了提取`hash`)
```
wget https://github.com/sanbei101/crack/releases/download/crack/john.zip
unzip -d john john.zip
```

## 提取为`HashCat`可识别的格式
```
awk -F: '{print $2}' raw_hash.txt > hash.txt
```

## 安装`HashCat`
```
wget https://github.com/sanbei101/crack/releases/download/crack/hashcat.zip
unzip -d hashcat hashcat.zip
```

## 使用`HashCat`
```
./hashcat/hashcat.bin -m 17200 -a 3 -w 4 \
  -i --increment-min 4 --increment-max 9 \
  hash.txt ?a?a?a?a?a?a?a?a?a
```