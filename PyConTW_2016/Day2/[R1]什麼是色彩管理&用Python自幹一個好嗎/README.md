## Talk: 什麼是色彩管理 & 用 Python 自幹一個好嗎 ?
- Info: https://tw.pycon.org/2016/events/talk/66630011804713004/
- Speaker: Kilik Kuo
- Slide : https://goo.gl/j0sS6z
- Questions: https://goo.gl/slides/s4uqbn

#### What is Color Management

在各個裝置上面轉換 color 的轉換系統

#### Why color Management
> Obtain a good match across color devices

我想要把鮮豔的紅傳遞給每一個人，不要有色偏，讓大家有相同的 experience

MAC OS >>>>>> Windows

[Kilik] 補充,
Mac 上由於 OSX framework stack 內建了 color management compoent "ColorSync" [1][2],
在Application 層開發透過系統提供的 API 時都會經過 ColorSync 做轉換, 省卻不少問題.
Windows 上則有 WIC [3] (win7以前) 用來擷取影像色彩資訊, WIA/WCS [4][5] (win8之後)給應用層使用.
註 : Windows 內建的 image viewer 有做 Color management, 小畫家沒有, 可以用來開圖測試 :)

[1] https://developer.apple.com/library/mac/technotes/tn2115/_index.html
[2] https://developer.apple.com/library/mac/documentation/GraphicsImaging/Reference/ColorSync_Manager/
[3] https://msdn.microsoft.com/zh-tw/library/windows/desktop/ee719902%28v=vs.85%29.aspx
[4] https://msdn.microsoft.com/en-us/library/windows/hardware/ff542835%28v=vs.85%29.aspx
[5] https://msdn.microsoft.com/library/windows/desktop/dd372231%28v=vs.85%29.aspx

#### Befor We Start - COLOR
Light > Eyes > Colors

Wavelength(nm) Blue -> Green -> Red (波長短到長)

天色變暗時，人類的尖銳敏銳度對紅色的辨色力會最先喪失

紅色有助於增快暗適應 （光適應 ~ 5min, 暗適應 ~ 20 min）

#### Befor We Start - CIE RGB matching function
- David Wright / John Guild's experiment
找一群健康的人，讓他們控制三個燈光（RGB）的比重，讓他們盡力控制燈光顏色比例來盡力調出他隨意指定的顏色
到最後算出一個公式，把色光的組合，用波長 input 來算出顏色
```
Color λ = r(λ') * R + g(λ') * G + b(λ') * B
R = 700nm, G = 546.1nm, B = 435.8nm
```

#### Before We Start - CIE XYZ(1931)

#### Before We Start - CIE XYZ(imaginary) to xyY(a cousin color space, visible in 2D)
- 定義**色度**座標(chromaticity)
```
x = X / (X + Y + Z)
y = Y / (X + Y + Z)
z = Z / (X + Y + Z) = 1 - x - y
X = (Y / y) * x
Z = (Y / y) * (1 - x - y)
```

#### Before We Start - Define RGB color Space Matrix in XYZ
- Specify a RGB color space matrix
	- Reddest red / Greenest green / Bluest blue
	- 3  vertices
	要找到三個覺得最紅、最綠、最藍 的點

- 定義黑白
	- Darkest dark / Lighest light
	- A space where Y1 < Y2

- RGB from XYZ
	- Define (0, 0, 0) -> (1, 1, 1)
		- 000(black) / 100(red) / 010(blue) / 001(green)
		- 111(white) ... 110 / 101 / 011
		- 8 vertices, 6 sides

> 所以我們可以藉由 color management ，跳到其他 color space 而不會有 color(data) loss

#### Before We Start - Reference white point
- 什麼是參考白
	- What we perceived as 'white' depends on the type of light that's illuminating a scene

- D50 / 5003K, D65 / 6504 K
	- Changing colors to match a new ref. white is called **adaptation**.
	- K (KelvinScale)

#### Before - ICC Profile ( 定義 RGB 的 space )
定義白點是甚麼、定義 RGB、 ...，預設的白點是 D50

#### Before - TRC( Tone Response Curve )
- 25 個燈泡，一個代表 RGB + 10
- 25 盞燈全開 = Max value
- 人類對於低暗度的變化感受比較強，高亮度變化比較弱
- ICC profile 裡面會放 curve，表示變化的曲線

#### Color Managment Flow
1. Non-linear Color space A
2. Linear Color Space A'
3. D65 - XYZ
4. D50 - XYZ
5. Linear Color Space B'
6. Non-linear Color space B

#### Pillow.ImageCms
- The ImageCms module
	- LittleCMS2 color management engine, based on PyCMS library.

#### ImageCms APIs
1. [Information] Profile Information
2. [Creation] Default profile
3. [Transformation] Directly from profile A to B
4. ... 

https://github.com/kilikkuo/Python_ColorManagement

[Kilik] answer to 用純 python 自幹一個, 好嗎 ?
A : 效能上來, 拜偷不要 Orz...
	但如果用一種追尋心靈平靜的角度來看, 還不錯 !  讓我挖掘了一段深刻的色彩與影像知識.
    1) 為了用 OpenCL 硬體加速轉換色彩空間, 需要一個 CPU 版本對照, 所以開始自幹.
    2) 為了確認 CPU 版本的正確性, 先得搞懂 Color Space & ICC Profile 相關知識, 然後自幹
    3) 為了讀取於影像中的 ICC profile, 用 python 開始寫 metadata parser, 又是一個 K spec後自幹.
    4) 為了不讓演講沒有太多 python, 找一個別人寫的 python CMM 使用看看.
    對我來說, frameworks / tools 的汰換日新月異, 除了"知道"這些春筍, 找一個題目往下挖掘1~3年,
	整個人生的職涯可以累積數個"根基穩固"的技術本, 甚至能在其他工作經驗中交互發揮, 很有好處, 
	分享一點心得給大家.