# HomeKit-PetSurveillance

PetSurveillance with Camera and TemperatureSensor, access by Homekit.

Two Part:
* endpoint
    
    Use `ESP32-CAM` , export camera video for RTSP stream , and export temperature data for JSON.

* collect

    Use container running, working to collect data from endpoint, and simulate HAP driver.

## 为什么要分为两部分

ESP32虽然支持片外 SPI RAM 但最高也才支持 4 MB

参考 [esp32-homekit-camera](https://github.com/maximkulkin/esp32-homekit-camera) 这个项目  当流媒体分辨率为 160x120，可以提供大约 1-2 fps；而将 VIDEO_IMAGE_SCALE_DENOM 设置为 2，流媒体分辨率变成 320x240 这时仅剩 0.5 fps 这是不能接受的

将 HomeKit 的部分抽出至别的设备上运行 节约ESP32上宝贵的RAM空间 无疑是解决帧率效率低下的一个好办法