# waveshare-s3-rlcd-4.2编译和刷写说明
## 1.视频：

https://www.bilibili.com/video/BV1kPF1z7Ewm/?spm_id_from=333.1391.0.0&vd_source=ea4a38c2402e8ebeaa9ec735833f7d68

## 2.编译固件

### (1)git仓库
```git
git clone https://github.com/ZhouhaoJiang/xiaozhi-esp32
cd xiaozhi-esp32
cp ./main/boards/waveshare-s3-rlcd-4.2/secret_config.h.example ./main/boards/waveshare-s3-rlcd-4.2/secret_config.h
```

### (2)填写和风天气 API 配置(secret_config.h)
``` 
> // 和风天气 API 配置
> // 申请地址：https://dev.qweather.com/
> #define WEATHER_API_KEY     "填写API_KEY"
> #define WEATHER_API_HOST    "填写API_HOST"
>
> // 时区配置
> // 格式参考：https://www.gnu.org/software/libc/manual/html_node/TZ-Variable.html
> // 常见值：
> //   中国 (UTC+8):  "CST-8"
> //   日本 (UTC+9):  "JST-9"
> //   美西 (UTC-8):  "PST8PDT"
> //   美东 (UTC-5):  "EST5EDT"
> #define TIMEZONE_STRING     "CST-8"
>
> // NTP 时间同步服务器
> // 国内推荐：ntp.aliyun.com / ntp.tencent.com
> // 海外推荐：pool.ntp.org / time.google.com
> #define NTP_SERVER          "ntp.aliyun.com"
```
### (3)编译固件
```docker run
docker run --rm -it -v $PWD:/project -w /project espressif/idf:v5.5.2 bash -c "source \$IDF_PATH/export.sh && python scripts/release.py waveshare-s3-rlcd-4.2 --name waveshare-s3-rlcd-4.2"
```
编译成果：./releases/

## 3.刷写固件

用flash_download_tool_3.9.9_R2.exe 刷写

选择
ChipType:ESP32-S3
WorkMode:Develop
LoadMode:UART
OK



第一行选择固件路径，地址：0x000
SPIFlashConfig
SPI SPEED：
80MHz
SPI MODE：QI0
DoNotChgBin  打勾

com 选择正确的端口 115200

START刷写，写完STOP

