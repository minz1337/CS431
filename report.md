<!-- Banner -->
<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: none;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>
<!-- Title -->
<h1 align="center"><b>TIỂU LUẬN MÔ HÌNH MÁY HỌC NÔNG</b></h1>
<h1 align="center"><b>LINEAR REGRESSION</b></h1>


## GIỚI THIỆU TIỂU LUẬN
* **Chủ đề báo cáo:** LINEAR REGRESSION
* **Tên môn học:** CÁC KỸ THUẬT HỌC SÂU VÀ ỨNG DỤNG
* **Mã môn học:** CS431
* **Mã lớp:** CS431.M21
* **Giảng viên:** **TS. Nguyễn Vinh Tiệp** 

## GIỚI THIỆU NHÓM

| STT | Họ tên | MSSV |
| :---: | --- | --- |
| 1 | Nguyễn Xuân Minh | 19522054 | 
| 2 | Hà Văn Thanh | 19522224 |
| 3 | Nguyễn Đức Thắng | 19522206 |
# **MỤC LỤC**

## **Giới thiệu**
  Trong cuộc sống hiện nay, hầu như ở mọi phương diện, chúng ta đều tìm cách tự động hóa tất cả mọi việc. Điều này không những góp phần làm giảm đi công sức chúng ta phải
  bỏ ra để thực hiện mà còn giúp công việc được thực hiện một cách bài bản, chuẩn xác nhất có thể. Giả sử chúng ta đang phát triển một phần mềm có thể dự đoán giá nhà cho một khu vực
  ở một thời điểm nhất định. Cụ thể là chúng ta có bài toán: một căn nhà rộng <img src="https://latex.codecogs.com/svg.image?&space;x_{1}" title="https://latex.codecogs.com/svg.image? x_{1}" /> <img src="https://latex.codecogs.com/svg.image?m^2" title="https://latex.codecogs.com/svg.image?m^2" />
  có <img src="https://latex.codecogs.com/svg.image?x_{2}" title="https://latex.codecogs.com/svg.image?x_{2}" /> phòng ngủ và cách trung tâm thành phố <img src="https://latex.codecogs.com/svg.image?x_{3}" title="https://latex.codecogs.com/svg.image?x_{3}" /> có 
  giá bao nhiêu. Giả sử chúng ta đã có số liệu thống kê từ 1500 căn nhà trong thành phố đó, liệu rằng khi có một căn nhà mới với các thông số về diện tích, số phòng ngủ và khoảng cách tới trung tâm, chúng ta có thể dự đoán được giá của căn nhà đó không? Nếu có thì 
  hàm dự đoán <img src="https://latex.codecogs.com/svg.image?y&space;=&space;f(x)" title="https://latex.codecogs.com/svg.image?y = f(x)" /> sẽ có dạng như thế nào ?
  
  Một cách đơn giản, chúng ta có thể thấy rằng:
  
  + Diện tích nhà càng lớn thì giá càng cao.
  + Số lượng phòng ngủ càng nhiều thì giá càng cao.
  + Càng xa trung tâm thành phố thì giá càng thấp.
  
  Như vậy, dường như 3 đại lượng trên có một mối quan hệ tuyến tính với giá nhà mà chúng ta cần dự đoán. Một hàm số đơn giản nhất có thể mô tả mối quan hệ giữa giá nhà và 3 đại lượng đầu vào là:
  
  <img src="https://latex.codecogs.com/svg.image?y\approx&space;f(x)&space;=&space;\tilde{y}" title="https://latex.codecogs.com/svg.image?y\approx f(x) = \tilde{y}" />
  
  <img src="https://latex.codecogs.com/svg.image?f(x)&space;=&space;w_{1}x_{1}&space;&plus;&space;w_{2}x_{2}&space;&plus;&space;w_{3}x_{3}&space;&plus;&space;w_{0}" title="https://latex.codecogs.com/svg.image?f(x) = w_{1}x_{1} + w_{2}x_{2} + w_{3}x_{3} + w_{0}" />
  
  Trong đó, <img src="https://latex.codecogs.com/svg.image?w_{1}" title="https://latex.codecogs.com/svg.image?w_{1}" />, <img src="https://latex.codecogs.com/svg.image?w_{2}" title="https://latex.codecogs.com/svg.image?w_{2}" />, <img src="https://latex.codecogs.com/svg.image?w_{3}" title="https://latex.codecogs.com/svg.image?w_{3}" />, <img src="https://latex.codecogs.com/svg.image?w_{0}" title="https://latex.codecogs.com/svg.image?w_{0}" /> là các hằng số mà chúng ta phải đi tìm.
