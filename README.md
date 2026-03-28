# waveshare-s3-rlcd-4.2编译和刷写说明
## 1.视频：

https://www.bilibili.com/video/BV1kPF1z7Ewm/?spm_id_from=333.1391.0.0&vd_source=ea4a38c2402e8ebeaa9ec735833f7d68

<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=116131805268112&bvid=BV1PsfhBCEqA&cid=36284664951&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>


## 2.编译固件

### (1)git仓库
```git
git clone https://github.com/ZhouhaoJiang/xiaozhi-esp32
cd xiaozhi-esp32
cp ./main/boards/waveshare-s3-rlcd-4.2/secret_config.h.example ./main/boards/waveshare-s3-rlcd-4.2/secret_config.h
```

### (2)填写和风天气 API 配置(secret_config.h)


申请地址：https://dev.qweather.com/
```
#define WEATHER_API_KEY     "填写API_KEY"
#define WEATHER_API_HOST    "填写API_HOST"
```

### (3)编译固件
```docker run
docker run --rm -it -v $PWD:/project -w /project espressif/idf:v5.5.2 bash -c "source \$IDF_PATH/export.sh && python scripts/release.py waveshare-s3-rlcd-4.2 --name waveshare-s3-rlcd-4.2"
```
固件位置：./releases/

## 3.刷写固件

用flash_download_tool_3.9.9_R2.exe 刷写

安装 Flash 下载工具：https://www.espressif.com.cn/zh-hans/support/download/other-tools。
或者直接下载下面这个压缩包解压打开就是[下载工具](https://my.feishu.cn/wiki/Zpz4wXBtdimBrLk25WdcXzxcnNS)
连接 ESP32 S3 开发板的 USB JTAG/serial 到电脑主机，运行 Flash 下载工具，使用 UART 模式把下载解压后的 merged-binary.bin 烧录到地址 0x0 。

```
选择
ChipType:ESP32-S3
WorkMode:Develop
LoadMode:UART
OK
```
![Image](https://github.com/wudingjian/waveshare-s3-rlcd-4.2/blob/main/screenshots/ila5a3-0.webp)

```
第一行选择固件路径，地址：0x000
SPIFlashConfig
SPI SPEED：
80MHz
SPI MODE：QI0
DoNotChgBin  打勾

com 选择正确的端口 115200
START刷写，写完STOP
```

![Image](https://github.com/wudingjian/waveshare-s3-rlcd-4.2/blob/main/screenshots/ilfdzy-0.webp)
