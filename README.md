## 安装`John`(为了提取`hash`)
```
sudo apt update && sudo apt install -y build-essential libssl-dev zlib1g-dev

git clone --depth 1 https://github.com/openwall/john -b bleeding-jumbo

cd john/src && ./configure && make -s clean && make -sj$(nproc)

./john/run/zip2john test.zip > raw_hash.txt // 替换为真实的zip文件名
```

## 提取为`HashCat`可识别的格式
```
awk -F: '{print $2}' raw_hash.txt > hash.txt
```

## 安装`HashCat`
```
sudo apt install hashcat
```

## 使用`HashCat`
```
./hashcat/hashcat.bin -m 17200 -a 3 -w 4 \
  -i --increment-min 4 --increment-max 9 \
  hash.txt ?a?a?a?a?a?a?a?a?a
```