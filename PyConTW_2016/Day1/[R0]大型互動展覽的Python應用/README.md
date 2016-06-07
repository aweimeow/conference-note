# Talk: 大型互動展覽的 Python 應用

- Info: https://tw.pycon.org/2016/events/talk/68743273514008626/
- Speaker: 陳炯廷

互動業 (？)
常用工具：OpenFramework / PureData / Kinect ...etc

#### 互動科技案例：
- 簽名自動雷雕成名牌
  HTML canvas => Django server => jpg file => 工讀生
- 解密科技寶藏
- 3D掃描

#### ID機
用Raspberry Pi 3
- Autoupdate要寫好
- Django (因為有admin所以非熟悉程式的人也可以用)
- zeroconf + avahi 自己找主機
- 使用 QRCode 設定機器 (ex. reboot 逼一下就重開)
- 全區開機、全區關機卡(實用！ pip install wakeonlan)
- 運用redis指令，可以摹擬很多人一起使用系統
- socket.io emitter 可以和場內server聯絡

#### 文件
因為不同公司有不同權限，Django和nginx串接來解決

去一個展場，需要安裝一個 App ，然後可能還沒看完，就離開了， App 又需要送審，相對於網頁，網頁打開就可以 work。