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
  ## **Mô hình Linear Regression**
  ### **Dạng của mô hình**
  Ở phương trình trên, nếu chúng ta đặt <img src="https://latex.codecogs.com/svg.image?w&space;=&space;[w_{0},w_{1},w_{2},w_{3}]^T" title="https://latex.codecogs.com/svg.image?w = [w_{0},w_{1},w_{2},w_{3}]^T" /> là vector (cột) hệ số cần phải tối ưu, <img src="https://latex.codecogs.com/svg.image?\overline{x}&space;=&space;[1,x_{1},x_{2},x_{3}]" title="https://latex.codecogs.com/svg.image?\overline{x} = [1,x_{1},x_{2},x_{3}]" /> là vector (hàng) dữ liệu đầu vào mở rộng (Số 1 được thêm vào đầu vector để tiện hơn trong quá trình tính toán).
  ### **Sai số dự đoán**
  Gọi e là sai số dự đoán giữa giá trị thực y và giá trị dự đoán <img src="https://latex.codecogs.com/svg.image?\hat{y}" title="https://latex.codecogs.com/svg.image?\hat{y}" />. Điều chúng ta mong muốn là giá trị e càng nhỏ càng tốt, tức là giá trị dự đoán xấp xỉ giá trị thực.
  
  Ban đầu, hàm sai số dự đoán được thiết kế là <img src="https://latex.codecogs.com/svg.image?e&space;=&space;y&space;-&space;\hat{y}" title="https://latex.codecogs.com/svg.image?e = y - \hat{y}" /> , đây là một hàm thiết kế còn "ngây thơ", vì với phương trình này, <img src="https://latex.codecogs.com/svg.image?e&space;=&space;y&space;-&space;\hat{y}" title="https://latex.codecogs.com/svg.image?e = y - \hat{y}" /> có thể âm, e nhỏ nhất là âm vô cực, nhưng sự sai lệch lại rất lớn.
  
  Kế đến, chúng tôi có thể lấp đầy sai lầm đó bằng cách thêm trị tuyệt đối vào biểu thức, hàm dự đoán trở thành <img src="https://latex.codecogs.com/svg.image?e&space;=&space;\left|y&space;-\hat{y}&space;\right|" title="https://latex.codecogs.com/svg.image?e = \left|y -\hat{y} \right|" />, hàm này tuy phản ánh được chính xác sai số, nhưng lại khó khăn trong việc tính đạo hàm (đạo hàm không liên tục trên toàn bộ tập xác định).
  
  Cuối cùng, chúng tôi tính <img src="https://latex.codecogs.com/svg.image?e^2&space;=&space;\frac{1}{2}*&space;(y&space;-&space;\hat{y})" title="https://latex.codecogs.com/svg.image?e^2 = \frac{1}{2}* (y - \hat{y})" />, trong đó, hệ số <img src="https://latex.codecogs.com/svg.image?\frac{1}{2}" title="https://latex.codecogs.com/svg.image?\frac{1}{2}" /> để thuận tiện trong quá trình tính toán (sẽ bị triệt tiêu khi tính đạo hàm)
  
 ### **Hàm mất mát**
 Điều tương tự xảy ra với các cặp (input,outcome), điều chúng ta muốn là tổng sai số của các cặp là nhỏ nhất, điều này tương đương với việc tìm **w** để hàm số sau đây đạt giá trị nhỏ nhất.
 
<img src="https://latex.codecogs.com/svg.image?\pounds(w)&space;=&space;\frac{1}{2}\sum_{i=1}^{N}&space;(y_{i}-\overline{x_{i}}w)^2" title="https://latex.codecogs.com/svg.image?\pounds(w) = \frac{1}{2}\sum_{i=1}^{N} (y_{i}-\overline{x_{i}}w)^2" />

Giá trị **w** làm cho hàm mất mát đạt giá trị nhỏ nhất được gọi là điểm tối ưu, kí hiệu :

<img src="https://latex.codecogs.com/svg.image?w^*&space;=&space;arg\displaystyle&space;\min_{&space;w}\pounds&space;(w)" title="https://latex.codecogs.com/svg.image?w^* = arg\displaystyle \min_{ w}\pounds (w)" />

### **Nghiệm của bài toán**

Để tìm nghiệm cho bài toán tối ưu, chúng ta tiến hành giải phương trình đạo hàm bằng 0. Đạo hàm theo **w** của hàm mất mát là:

<img src="https://latex.codecogs.com/svg.image?\frac{\partial\pounds&space;(w)&space;}{\partial&space;w}&space;=&space;\bar{X}^T(\bar{X}w&space;-&space;y)" title="https://latex.codecogs.com/svg.image?\frac{\partial\pounds (w) }{\partial w} = \bar{X}^T(\bar{X}w - y)" />

Phương trình đạo hàm bằng 0 tương đương với:

<img src="https://latex.codecogs.com/svg.image?\bar{X}^T\bar{X}w&space;=&space;\bar{X}^Ty&space;=&space;b" title="https://latex.codecogs.com/svg.image?\bar{X}^T\bar{X}w = \bar{X}^Ty = b" />

- Nếu ma trận <img src="https://latex.codecogs.com/svg.image?A&space;=&space;\bar{X}^T\bar{X}" title="https://latex.codecogs.com/svg.image?A = \bar{X}^T\bar{X}" /> khả nghịch (định thức khác 0), thì phương trình có nghiệm duy nhất <img src="https://latex.codecogs.com/svg.image?w&space;=&space;A^{-1}b" title="https://latex.codecogs.com/svg.image?w = A^{-1}b" />.
- Ngược lại, phương trình có nghiệm <img src="https://latex.codecogs.com/svg.image?w&space;=&space;A^\dagger&space;b&space;=&space;(\bar{X}^T\bar{X})^\dagger&space;\bar{X}^T&space;y" title="https://latex.codecogs.com/svg.image?w = A^\dagger b = (\bar{X}^T\bar{X})^\dagger \bar{X}^T y" />
## **Cài đặt chương trình**
Giả sử chúng ta có một bảng dữ liệu thời gian sinh trưởng và chiều cao của một loài cây như sau
   
| STT | Thời gian sinh trưởng (năm) | chiều cao (cm) |
| :---: | --- | --- |
| 1 | 4.5 | 147 | 
| 2 | 5.0 | 150 |
| 3 | 5.1|	153 |
| 4 | 5.2 | 155 |
| 5 | 5.4 | 158 |
| 6 | 5.6 | 160 |
| 7 | 5.8 | 163 |
| 8 | 5.9 | 165 |
| 9 | 6.0 | 168 |
| 10 | 7.2 | 170 |
| 11| 6.3 | 173 |
|12 | 6.4 | 175 |
| 13 | 6.7 | 178 |
| 14| 6.8 | 180 |
| 15| 6.9 | 183 |

Bài toán đặt ra là: liệu có thể dự đoán chiều cao của cây dựa vào thời gian trồng hay không ?
-> Chúng ta có thể thấy thời gian trồng cây tỉ lệ thuận với chiều cao của cây (sẽ không đúng trong thực tế) nên có thể sử dụng Linear Regression để dự đoán cho bài toán này.
Chúng ta sẽ giữ lại cột 5.2 và 5.6 cho việc kiểm tra tính đúng đắn của mô hình.

### **Trực quan hóa dữ liệu**
Trước tiên, chúng ta cần 2 thư viện **numpy** cho đại số và **matplotlib** cho việc vẽ hình:

    import numpy as np 
    import matplotlib.pyplot as plt
    
Tiếp theo, chúng ta sẽ trực quan hóa dữ liệu trên đồ thị

    # height (cm)
    y = np.array([[147, 150, 153, 158, 163, 165, 168, 170, 173, 175, 178, 180, 183]]).T
    # Time (year)
    X = np.array([[ 4.9, 5.0, 5.1,  5.4, 5.8, 5.9, 6.0, 6.2, 6.3, 6.4, 6.6, 6.7, 6.8]]).T
    # Visualize data 
    plt.plot(X, y, 'ro')
    plt.axis([4, 7.5, 140, 190])
    plt.xlabel('Height (cm)')
    plt.ylabel('Time(year)')
    plt.show()
    
![alt text](https://github.com/minz1337/CS431/blob/main/GD1/source/1.png)

Từ đồ thị này, ta có thể thấy dữ liệu được sắp xếp gần như một đường thẳng, vậy mô hình LR có khả năng sẽ cho kết quả tốt.
Chiều_cao = w_0* thời_gian + w_1
### **Nghiệm theo công thức**

    # Building Xbar 
    one = np.ones((X.shape[0], 1))
    Xbar = np.concatenate((one, X), axis = 1)

    # Calculating weights of the fitting line 
    A = np.dot(Xbar.T, Xbar)
    b = np.dot(Xbar.T, y)
    w = np.dot(np.linalg.pinv(A), b)
    print('w = ', w)
    # Preparing the fitting line 
    w_0 = w[0][0]
    w_1 = w[1][0]
    x0 = np.linspace(4, 8, 2)
    y0 = w_0 + w_1*x0

    # Drawing the fitting line 
    plt.plot(X.T, y.T, 'ro')     # data 
    plt.plot(x0, y0)               # the fitting line
    plt.axis([4, 7.5, 140, 190])
    plt.xlabel('Height (cm)')
    plt.ylabel('Time(year)')
    plt.show()
    
    w =  [[60.91228332]
    [17.7839211 ]]
![alt text](https://github.com/minz1337/CS431/blob/main/GD1/source/2.png)

Từ đồ thị trên, ta thấy mô hình hoạt động khá tốt. Tiếp theo chúng ta sẽ thử với 2 giá trị test.
    
    
    y1 = w_1*5.2 + w_0
    y2 = w_1*5.6 + w_0

    print( u'Chieu cao cua cay co thoi gian 5.2(nam) la: %.2f (kg), real number: 155 (kg)'  %(y1) )
    print( u'Chieu cao cua cay co thoi gian 5.6(nam) la: %.2f (kg), real number: 160 (kg)'  %(y2) )
    
    
    Chieu cao cua cay co thoi gian 5.2(nam) la: 153.39 (kg), real number: 155 (kg)
    Chieu cao cua cay co thoi gian 5.6(nam) la: 160.50 (kg), real number: 160 (kg)
    
Chúng ta thấy rằng, kết quả dự đoán khá gần so với thực tế.
## **Bài tập**
Giả sử chúng ta muốn kinh doanh bán thức ăn theo hình thức xe bán thức ăn. Câu hỏi đặt ra rằng liệu nên bán ở đâu thì cho được lợi nhuận cao. Vậy khi chúng ta biết được thành phố có mật độ dân số thì có thể dựa vào đó để tính được lợi nhuận hay không? Để kiểm chứng điều đó, nhóm thu thập được bộ dataset gồm dân số của các thành phố và lợi nhuận thu được ứng với mỗi thành phố đó.

Input: X dân số (X>=0)

Output: y lợi nhuận dự đoán được dựa trên dân số (y>=0)

Souce code [Link here](https://github.com/minz1337/CS431/blob/main/BaiTap_Linear_Regression.ipynb)
## **Kết luận**
### **Ưu điểm của mô hình**
Linear Regression là một mô hình đơn giản, dễ cài đặt, lời giải cho phương trình đạo hàm bằng 0 cũng khá đơn giản.
### **Nhược điểm của mô hình**
- Linear Regression rất nhạy cảm với nhiễu (sensitive to noise). Vì vậy, trước khi thực hiện Linear Regression, các nhiễu (outlier) cần phải được loại bỏ. Bước này được gọi là tiền xử lý (pre-processing).
- nó không biễu diễn được các mô hình phức tạp. Mặc dù trong phần trên, chúng ta thấy rằng phương pháp này có thể được áp dụng nếu quan hệ giữa outcome và input không nhất thiết phải là tuyến tính, nhưng mối quan hệ này vẫn đơn giản nhiều so với các mô hình thực tế.
- Khi dữ liệu lớn công thức hiện tại có độ phức tạp lớn  để tính ma trận nghịch đảo.
    
    
