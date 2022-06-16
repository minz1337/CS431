<!-- Banner -->
<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: none;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>
<!-- Title -->
<h1 align="center"><b>TIỂU LUẬN MÔ HÌNH MÁY HỌC SÂU GĐ3</b></h1>
<h1 align="center"><b>KIẾN TRÚC MẠNG RNN</b></h1>


## GIỚI THIỆU TIỂU LUẬN
* **Chủ đề báo cáo:** KIẾN TRÚC MẠNG RNN
* **Tên môn học:** CÁC KỸ THUẬT HỌC SÂU VÀ ỨNG DỤNG
* **Mã môn học:** CS431
* **Mã lớp:** CS431.M21
* **Giảng viên:** **TS. Nguyễn Vinh Tiệp** 

## GIỚI THIỆU NHÓM

| STT | Họ tên | MSSV |
| :---: | --- | --- |
| 1 | Nguyễn Xuân Minh | 19521848 | 
| 2 | Hà Văn Thanh | 19522224 |
| 3 | Nguyễn Đức Thắng | 19522206 |

## NỘI DUNG BÀI BÁO CÁO

### Mạng hồi quy RNN

  Để có thể hiểu rõ về RNN, trước tiên chúng ta cùng nhìn lại mô hình Neural Network dưới đây:
  
  
  Như đã biết thì Neural Network bao gồm 3 phần chính là Input layer, Hidden layer và Output layer, ta có thể thấy là đầu vào và đầu ra của mạng neuron này là độc lập với nhau. Như vậy mô hình này không phù hợp với những bài toán dạng chuỗi như mô tả, hoàn thành câu, ... vì những dự đoán tiếp theo như từ tiếp theo phụ thuộc vào vị trí của nó trong câu và những từ đằng trước nó. 
  
  Chính vì vậy, RNN ra đời với ý tưởng chính là sử dụng một bộ nhớ để lưu lại thông tin từ từ những bước tính toán xử lý trước để dựa vào nó có thể đưa ra dự đoán chính xác nhất cho bước dự đoán hiện tại.
  
### Tổng quan mô hình RNN

Nếu như mạng Neural Network chỉ là input layer <img src="https://latex.codecogs.com/svg.image?x" title="https://latex.codecogs.com/svg.image?x" /> đi qua hidden layer <img src="https://latex.codecogs.com/svg.image?h" title="https://latex.codecogs.com/svg.image?h" /> và cho ra output layer <img src="https://latex.codecogs.com/svg.image?y" title="https://latex.codecogs.com/svg.image?y" /> với full connected giữa các layer thì trong RNN, các input <img src="https://latex.codecogs.com/svg.image?x_{t}" title="https://latex.codecogs.com/svg.image?x_{t}" /> sẽ được kết hợp với hidden layer <img src="https://latex.codecogs.com/svg.image?h_{t-1}" title="https://latex.codecogs.com/svg.image?h_{t-1}" />  bằng hàm  <img src="https://latex.codecogs.com/svg.image?f_{w}" title="https://latex.codecogs.com/svg.image?f_{w}" /> để tính toán ra hidden layer <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" /> hiện tại và output <img src="https://latex.codecogs.com/svg.image?y_{t}" title="https://latex.codecogs.com/svg.image?y_{t}" /> sẽ được tính ta từ <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" />, **W** là tập các trọng số và nó được ở tất cả các cụm, các <img src="https://latex.codecogs.com/svg.image?L_{1},&space;L_{2},...&space;L_{t}" title="https://latex.codecogs.com/svg.image?L_{1}, L_{2},... L_{t}" /> là các hàm mất mát. Như vậy kết quả từ các quá trình tính toán trước đã được "nhớ" bằng cách kết hợp thêm <img src="https://latex.codecogs.com/svg.image?h_{t-1}" title="https://latex.codecogs.com/svg.image?h_{t-1}" /> để tính 
<img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" /> để tăng độ chính xác cho những dự đoán ở hiện tại.


Cụ thể quá trình tính toán sẽ là:

<img src="https://latex.codecogs.com/svg.image?h_{t}&space;=&space;f_{w}&space;(h_{t-1},x_{t})" title="https://latex.codecogs.com/svg.image?h_{t} = f_{w} (h_{t-1},x_{t})" />

Thường thì <img src="https://latex.codecogs.com/svg.image?f_{w}" title="https://latex.codecogs.com/svg.image?f_{w}" /> sẽ sử dụng hàm **tanh**, công thức trên sẽ trở thành:

<img src="https://latex.codecogs.com/svg.image?h_{t}=&space;tanh(W_{hh}h_{t-1}&plus;W_{xh}x_{t})" title="https://latex.codecogs.com/svg.image?h_{t}= tanh(W_{hh}h_{t-1}+W_{xh}x_{t})" />

<img src="https://latex.codecogs.com/svg.image?y_{t}&space;=&space;W_{hy}h_{t}" title="https://latex.codecogs.com/svg.image?y_{t} = W_{hy}h_{t}" />

Đến đây có 3 thứ mới xuất hiện: <img src="https://latex.codecogs.com/svg.image?W_{xh},&space;W_{hh},&space;W_{hy}" title="https://latex.codecogs.com/svg.image?W_{xh}, W_{hh}, W_{hy}" />. Đối với mạng NN thông thường, chỉ sử dụng một trọng số **W** duy nhất thì với RNN, nó sử dụng 3 ma trận trọng số cho 2 quá trình tính toán: <img src="https://latex.codecogs.com/svg.image?W_{hh}" title="https://latex.codecogs.com/svg.image?W_{hh}" /> kết hợp với bộ nhớ trước <img src="https://latex.codecogs.com/svg.image?h_{t-1}" title="https://latex.codecogs.com/svg.image?h_{t-1}" /> và <img src="https://latex.codecogs.com/svg.image?W_{xh}" title="https://latex.codecogs.com/svg.image?W_{xh}" /> kết hợp với <img src="https://latex.codecogs.com/svg.image?x_{t}" title="https://latex.codecogs.com/svg.image?x_{t}" /> để tính ra bộ nhớ cho bước hiện tại <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" /> từ đó kết hợp với <img src="https://latex.codecogs.com/svg.image?W_{h}y" title="https://latex.codecogs.com/svg.image?W_{h}y" /> để tính ra <img src="https://latex.codecogs.com/svg.image?y_{t}" title="https://latex.codecogs.com/svg.image?y_{t}" /> .

### Các dạng của mô hình RNN
  Cũng giống như các mô hình khác, RNN có nhiều dạng, biến thể khác nhau để phù hợp với từng bài toán cụ thể, dưới đây là một số dạng của mô hình RNN cơ bản:
  
  
  
  **One to One**: là dạng bài toán chỉ có một đầu vào (input) và một đầu ra (ouput). Đây là mẫu bài toán cho Neural Network (NN) và Convolutional Neural Network (CNN). Có thể kể đến các bài toán điển hình như bài toán phân loại hình ảnh: Input là 1 ảnh và output là 1 ảnh đã được segment.
  
  **One to many**: là dạng bài toán chỉ có một đầu vào (input) nhưng có nhiều đầu ra (ouput). Có thể kể đến bài toán captioning cho ảnh: input là một ảnh, output là những từ được kết hợp lại thành một câu để mô tả cho ảnh đấy.
  
  **Many to one**: là dạng bài toán có nhiều đầu vào (input) nhưng chỉ có một đầu ra (output). Có thể kể đến bài toán phân loại hành động trong video: input là từng frame của một video, output là loại hành động xảy ra trong video đó.
  
  **Many to many**: là dạng bài toán có nhiều đầu vào (input) và có nhiều đầu ra (output). Có thể kể đến bài toán dịch máy, ví dụ trong bài toán dịch từ tiếng việt sang tiếng anh, input là một câu gồm nhiều chữ tiếng việt, output cũng là một câu nhiều chữ tiếng anh được dịch ra từ câu tiếng việt input.
  
  ### Các ứng dụng của bài toán sử dụng mô hình RNN
  **Speech to Text**:Chuyển giọng nói sang text.
  
  **Sentiment classification**: Các dạng bài toán phân loại.
  
  **Video recognition**: Nhận diện hành động trong video.
  
  **Machine translation**: Dịch tự động giữa các ngôn ngữ
  
  ...
  
  Ngoài ra, vẫn còn nhiều ứng dụng khác của mô hình RNN trong nhiều khía cạnh, nhiều lĩnh vực khác nhau.
  
  ### Ưu & Nhược điểm của mô hình:
  
  **Ưu điểm**
  
  - Khả năng xử lí đầu vào với bất kì độ dài nào.
  
  - Kích cỡ mô hình không tăng theo kích cỡ đầu vào.

  - Quá trình tính toán sử dụng các thông tin cũ.
  
  - Trọng số được chia sẻ trong suốt thời gian.
  
 **Nhược điểm**
 
 - Tính toán chậm.
 
 - Khó để truy cập các thông tin từ một khoảng thời gian dài trước đây.

 - Không thể xem xét bất kì đầu vào sau này nào cho trạng thái hiện tại.

### Code Minh họa

[![Open in colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1DZox3ZzNHOsDTe8WMygIO-b-yxj55zWe?usp=sharing)
 
