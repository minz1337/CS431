<!-- Banner -->
<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: none;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>
<!-- Title -->
<h1 align="center"><b>TIỂU LUẬN MÔ HÌNH MÁY HỌC SÂU</b></h1>
<h1 align="center"><b>KIẾN TRÚC MẠNG RNN VỚI ATTENTION</b></h1>


## GIỚI THIỆU TIỂU LUẬN
* **Chủ đề báo cáo:** KIẾN TRÚC MẠNG RNN VỚI ATTENTION
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

## NỘI DUNG BÀI BÁO CÁO

### GIỚI THIỆU - NGUYÊN NHÂN ATTENTION RA ĐỜI
  Chúng ta sử dụng các từ như thế nào? Nói một cách đơn giản, các từ được chúng ta sử dụng bằng cách nối các từ lại với nhau thành một chuỗi để tạo thành câu/ cụm từ có nghĩa. Đó là
  trong cuộc sống hằng ngày, còn trong tin học, cụ thể là về lĩnh vực "xử lý ngôn ngữ tự nhiên", để biểu diễn chuỗi này ở không gian vector, chúng ta cần tối thiểu
  2 chiều: một chiều để biêu diễn các từ, một chiều để biểu diễn thời gian xuất hiện của các từ đó. Lý do là chúng ta cần các từ khác nhau xuất hiện trong các thời 
  điểm khác nhau để diễn đạt ý tưởng của chúng ta bằng ngôn ngữ.
  
 Mạng nơ ron hồi quy (RNN) là mô hình ra đời để xử lý thông tin tạo nên bởi các chuỗi từ. Mô hình sẽ đi từ đầu đến cuối chuỗi để có được thông tin liên kết giữa các từ. Mặc dù là 
 mô hình tiên phong trong xử lí chuỗi nhưng vì tiếp nhận đầu vào không có chọn lọc nên mô hình này gặp vấn đề Vanishing Gradient, làm cho mô hình hoạt động không hiệu quả
 ở những câu/ đoạn văn bản dài. RNN dần bị lãng quên cho đến khi các biến thể của nó là LSTM và GRU ra đời giúp tăng cường khả năng ghi nhớ và hiệu quả của mô hình.
 Tuy nhiên, với sự phức tạp của LSTM, thì tốc độ train đã trở nên chậm hơn nhiều lần so với RNN. Vấn đề này ảnh hưởng đáng kể tới tốc độ xử lý để phát triển sản phẩm của 
 NLP nên LSTM cũng chưa được đánh giá cao.
 
 Và cuối cùng, kỹ thuật Attention ra đời, giải quyết hai vấn đề mà cả RNN và LSTM gặp phải là gặp khó khăn ghi ghi nhớ một câu dài, dẫn đến mất mát thông tin và do kiến 
 trúc tuần tự nên không thể tận dụng sức mạnh của GPU.
