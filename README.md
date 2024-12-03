
<div align="center">
  <img src="https://github.com/user-attachments/assets/659e8acc-2fda-4ad9-a9ac-525704fba4ee" width="100%" height="auto"/>
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.demolab.com?font=Montserrat&weight=700&size=19&pause=500&color=FFCE76&width=435&lines=Quy+trình+code+tool+auto+Python+Selenium" alt="Typing SVG" />
  </a>
</div>

> [!NOTE]
> # Danh mục:
> - [Giới thiệu](#1-giới-thiệu)
> - [Chuẩn bị](#2-chuẩn-bị)
> - [Làm quen với Selenium](#3-làm-quen-với-selenium)
> - [Thao tác](#4-thao-tác)
>   + [Thao tác nhấn](#đầu-tiên-là-thao-tác-nhấn)
>   + [Thao tác nhập](#tiếp-theo-là-thao-tác-nhập)


## 1. Giới thiệu
- **Tác giả**: [Verse](https://github.com/terris91)
- **Cột mốc thời gian**: 2024
- **Full Docs**: [Selenium with Python](https://selenium-python.readthedocs.io/) (gốc)
- **Đôi lời mình muốn nói trước khi bắt đầu**:
  + Các hướng dẫn cho Selenium tiếng Việt toàn ở phiên bản cũ thành ra mình làm DOC này cho phiên bản `>=4.0`.
  + Vì sao ư? Vì Selenium `4.0+` có cập nhật không cần dùng file `WebDriver.exe` nữa. (Ví dụ như: ChromeDriver.exe)
  + Mình chỉ tập trung vào tool auto nhập liệu là chính. (account checker, register)
  + Các docs khác toàn cho ví dụ là `https://example.com` rất trừu tượng, khó hiểu. Mình cho ví dụ cụ thể để bạn dễ nắm bắt hơn.
- **Ở DOC này mình sẽ dùng Chrome là trình duyệt chính vì tính phổ biến**.

## 2. Chuẩn bị
#### Trước khi bắt đầu vào việc code tool ta cần chuẩn bị những thứ như sau:
- [Python](https://www.python.org/): Nên cài đặt phiên bản `3.1x`. (Ở đây mình dùng `3.11`)
- Code-editor/IDE: Bất kì phần mềm nào, VSCode, Sublime Text, ... Và lưu ý là bạn hãy set up đầy đủ cho Python nhé. (Ở đây mình dùng [VSCode](https://code.visualstudio.com/) hoặc [Cursor](https://www.cursor.com/))
- [Selenium](https://pypi.org/project/selenium/): `pip install selenium`.
- Đã trang bị sẵn kiến thức Python cơ bản.
- Cuối cùng là một cái đầu tỉnh táo và một tư duy tốt cho việc code.

## 3. Làm quen với Selenium

<img width="50%" align='right' src="https://github.com/user-attachments/assets/4a5b4e53-20b1-467e-9aea-7554e9f6ff78">

- Đầu tiên là thư viện Selenium. Thư viện này giúp chúng ta tự động hoá các quá trình sử dụng trình duyệt. Giúp các bạn code tool auto (phần lớn là để nhập liệu hoặc auto-clicker).
- Các tool Python auto hiện nay sử dụng Selenium cực kỳ nhiều.
- Bắt đầu với thư viện. Ở phần import hãy chuẩn bị như sau (lưu ý là càng về sau thì còn sử dụng nhiều thư viện khác):
  ```python
  from selenium import webdriver
  from time import sleep
  import os
  from selenium.webdriver.common.by import By
  ```
  + Giải thích một chút, với dòng `from selenium import webdriver` chả có gì phải nói cả vì phải import module của selenium vào. Với phần time và os, khi thực hiện việc code auto, sẽ có các khoảng như website sẽ load tốn vài giây, rồi 1 khoảng nào đó cần thời gian để chạy thì ta dùng `sleep(x)` để delay lại với `x=giây`.
  + Với dòng `from selenium.webdriver.common.by import By`, ta dùng nó để tìm các phần tử (Element) trên các trang web. Ví dụ như các nút, các ô chứa nơi cần nhập liệu, cần bấm vào.
 
- Đến với những dòng code đầu tiên mình sẽ giới thiệu như sau:
  ```python
  from selenium import webdriver
  # Khởi tạo trình duyệt mà không cần chỉ định đường dẫn đến chromedriver
  driver = webdriver.Chrome() # driver là tên biến bạn đặt

  while True: # Vì sao while True pass? Vì sẽ có thể dính lỗi tự động bật trình duyệt lên xong một lúc là tắt trình duyệt
    pass # Việc dùng while true pass sẽ bảo dẩm khi việc bật trình duyệt lên và không bị tắt
  ```
+ Như bạn có thể đọc phần comment của code mình đã giải thích kỹ vì sao lại thế.
- Và để truy cập 1 web cụ thể thì làm như nào?
  + Đơn giản là thêm `driver.get('https://yourwebsite.com')` vào với `yourwebsite` là web bạn cần mở.
  ```python
    from selenium import webdriver
    # Khởi tạo trình duyệt mà không cần chỉ định đường dẫn đến chromedriver
    driver = webdriver.Chrome()
    driver.get('https://pinterest.com') # Truy cập web pinterest là một ví dụ

    while True:
      pass
  ```
  + Như ở trên mình dùng [Pinterest](https://pinterest.com) là một ví dụ cho trang web cần mở ra.
  + Được rồi, đến đây thì ta đã biết cách mở 1 web lên và giờ ta phải học cách thao tác với nó.
## 4. Thao tác:
#### Có rất nhiều thao tác bạn có thể làm với Selenium nhưng phần lớn là code tool check mail/pass,... Và mình sẽ giới thiệu nó trước
### Đầu tiên là thao tác nhấn:
  + Với thao tác nhấn, ta sẽ dùng code như sau:
    ```python
    driver.find_element(By.XPATH, '/html/body/header/div/div[2]/div[1]/a').click() # Element của nút login mà bạn thấy trên website Pinterest
    ```
  + Từ từ đã nào, chưa gì đã 1 dãy code dài như thế. Để mình giải thích
  + Với driver.find_element(By.XPATH, '') nó là thao tác xác định phần tử nằm ở đâu, và được tìm kiếm theo đường dẫn XPATH, hoặc là ID, hoặc NAME phụ thuộc vào thứ bạn tìm với phần `XPATH` được thay thế bới `ID`, `NAME`, ...

  + Đầu tiên bạn phải tự xác định các phần tử nằm ở dâu, thao tác tìm như sau:
  <p align="center"><img src="https://github.com/user-attachments/assets/5752f2d1-b0f0-4877-8fc0-3339e08a4adc" width="80%" height="auto"/></p>
  <p align="center"><i>Nút login ở đây</i></p>
  
  + Bạn sẽ nhấn `F12` (hoặc chuột phải, chọn `Inspect`) sau đó nhấn `Ctrl Shift C` (hoặc ấn vào cái biểu tượng chọn phần tử)
  <p align="center"><img src="https://github.com/user-attachments/assets/f9807501-8a82-425b-b63f-674668684c58" width="80%" height="auto"/></p>
  <p align="center"><i>Nhấn vào công cụ tìm thông tin element này</i></p>

  + Sau khi nhấn vào công cụ ấy xong, thì ấn vào nút login hay bất cứ phần tử nào khác về sau và nó sẽ hiện ra đoạn code chứa phần tử đó trang bên cạnh
  <p align="center"><img src="https://github.com/user-attachments/assets/72221450-f470-4487-9c18-47cbb4d4cb9a" width="80%" height="auto"/></p>
  <p align="center"><i>Thông tin của element nằm ở đây</i></p>
  
  + Được rồi, tiếp theo đó tại phần tử đang được trỏ vào, ta nhấn chuột phải và đưa chuột vào nút copy, chọn Copy XPATH. Nó sẽ có dạng đường dẫn như sau `//*[@id="__PWS_ROOT__"]/div/div[1]/div/div[1]/div/div[2]/div[2]/button/div/div`
  <p align="center"><img src="https://github.com/user-attachments/assets/de6246c6-c653-4f56-b36e-7924f6d875d1" width="80%" height="auto"/></p>
  <p align="center"><i>Copy XPATH</i></p>
  
  + Rồi đó, copy và dán vào thôi nó sẽ ra `driver.find_element(By.XPATH, '/html/body/header/div/div[2]/div[1]/a').click()`
  + Và hàm `.click()` là để nhấn vào (quá rõ ràng)
  + Tương tự bạn sẽ biết là sau khi nhấn vào login sẽ sẽ hiện ra 1 ô đăng nhập
  + Mình có một lưu ý nhỏ ở đây là các bạn phải tự tư duy, lấy phần tử cũng như tự hình dung trong đầu các thao tác
  + Một số web nó sẽ gộp phần đăng ký và đăng nhập vào một nút, xong phải nhấp tiếp nút đăng nhập, lúc này cần set delay với `sleep()` (hoặc là không bạn có thể cân xét)
  + Khó hiểu quá à? Ví dụ ở đây mình sẽ dùng website `https://client.123host.vn/` với nút đăng nhập nó lại nằm trong 1 nút dăng nhập khác. Khi đó ta thực hiện code như sau
    ```python
    driver.find_element(By.XPATH, '/html/body/header/div/div[2]/div[1]/a').click() # Nút đăng nhập thứ nhất
    time.sleep(1) # Delay 1 giây (Nhớ import time lên đầu file code)
    driver.find_element(By.XPATH,'/html/body/header/div/div[2]/div[1]/ul/div/li[2]/a').click() # Nút đăng nhập thứ hai
    ```
> [!TIP]
  > Bạn nên viết 1 hàm click để rút gọn lại code cho dễ đọc
  > ```python
  > def click(xpath):
  >  driver.find_element(By.XPATH, xpath).click()
  > click('/html/body/div[2]/div/div[2]/div[1]/div/div[1]/button')
  > ```
  <p align="center"><img src="https://github.com/user-attachments/assets/0b30767a-8212-41c7-8881-529b8b801e0a" width="80%" height="auto"/></p>
  <p align="center"><i>Nói chung là phải tự tư duy nhé :)</i></p>
  
### Tiếp theo là thao tác nhập:
  <img width="40%" align='right' src="https://github.com/user-attachments/assets/019e1207-9588-4059-a14c-a6b76efb8016">
  
  + Với phần nhập, ở mức cơ bản ta dùng hàm `send_keys("...")` với `...` là thứ bạn muốn nhập
  + Thường là username hoặc mail gì đó và password
  + Công việc lấy phần tử sẽ tương tự nhưng khác một chút về vấn đề thay vì dùng XPATH ta dùng `ID` hoặc `NAME` hoặc một vài các phần tử khác như hình bên
  + Bạn phải tự suy nghĩ mình sẽ lấy phần nào
  + Ở đây trong website `https://pinterest.com` mình sẽ lấy `ID` với `email` và `password`

 
<details>
  <summary>Show các phần tử</summary>

- `By.XPATH`
- `By.ID`
- `By.NAME`
- `By.CSS_SELECTOR`
- `By.CLASS_NAME`
- `By.TAG_NAME`
- `By.LINK_TEXT`
- `By.PARTIAL_LINK_TEXT`
- `By.CUSTOM`

</details>

  <p align="center"><img src="https://github.com/user-attachments/assets/aaf12970-1ec5-41fe-88ea-a96867f7a99a" width="80%" height="auto"/></p>
  <p align="center"><i>Tương tự</i></p>
  <p align="center"><img src="https://github.com/user-attachments/assets/e3c5a18d-c129-48d5-ab65-d726da1f76b5" width="80%" height="auto"/></p>
  <p align="center"><i>Lấy ID là email</i></p>

  + Thì ở đây mình dùng phần tử `ID="email"` để dùng
  + Do đó ta có đoạn code như sau `driver.find_element(By.ID, 'email').send_keys("tendangnhap@mail.com")`
  + Và tương tự với password `driver.find_element(By.ID, 'password').send_keys("matkhaucuatoi)`
  + Mặt khác, ta có thể tìm theo `NAME` ví dụ như ở website `https://client.123host.vn/` ta code như sau:
    ```python
    driver.find_element(By.NAME, 'username').send_keys("tendangnhap@mail.com")
    driver.find_element(By.NAME, 'password').send_keys("matkhaucuatoi)
    ```
  + Đơn giản là thay `ID` bằng `NAME` thôi và nhớ phải theo đúng `NAME="username"`. Là username chứ không phải email như Pinterest.
  <p align="center"><img src="https://github.com/user-attachments/assets/c2175cce-5e0a-4c40-8530-c16f2eb34616" width="80%" height="auto"/></p>
  <p align="center"><i>NAME</i></p>
<p align="center"><i>Còn tiếp...</i><p/>
