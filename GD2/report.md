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
 Tuy nhiên, với sự phức tạp của LSTM, thì tốc độ train đã trở nên chậm hơn nhiều lần so với RNN. Vấn đề này ảnh hưởng đáng kể tới tốc độ xử lý để phát triển sản phẩm của NLP nên LSTM cũng chưa được đánh giá cao. Và cuối cùng, kỹ thuật Attention ra đời, giải quyết hai vấn đề mà cả RNN và LSTM chưa thể thực sự làm tốt.
  Để hiểu rõ cụ thể cơ chế Attention, nhóm bọn em xin tìm hiểu cụ thể về cơ chế này trong bài toán dịch máy (NMT).
 
 ### MÔ HÌNH SEQUENCE TO SEQUENCE
  Một mô hình Sequence to Sequence chuyển hóa một chuỗi đầu vào thành một vector có chiều dài cố định, sau đó sử dụng một mạng RNN để giải mã vector này thành chuỗi đích. Mô hình gồm có một bộ Encoder và một bộ Decoder. Trong đó Encoder sẽ chuyển hóa chuỗi đầu vào thành một véc tơ cố định, và Decoder sử dụng véc tơ cố định này để tạo thành chuỗi đầu ra.
  
  Ví dụ với chuỗi đầu vào “What are you doing ?”, RNN duyệt qua từng phần tử của chuỗi đầu vào, ở mỗi thời điểm RNN nhận vào một phần tử của chuỗi và trạng thái ẩn của thời điểm trước đó. Đến cuối cùng, vector trạng thái ẩn đầu ra của RNN sau khi duyệt qua phần tử cuối cùng cũng sẽ là véc tơ đầu ra của Encoder. Vector cuối cùng này được gọi là Encoder vector, được coi là chứa các thông tin được tóm gọn lại của chuỗi đầu vào.
  
  Decoder cũng sử dụng RNN để giải mã Encoder vector. Ở thời điểm đầu tiên Decoder nhận đầu vào là Encoder véc tơ và _START token (_START và _END là hai phần tử đặc biệt dùng để đánh dấu điểm bắt đầu và kết thúc câu), sau đó ở các thời điểm tiếp theo RNN sẽ lấy đầu ra của thời điểm trước cùng với véc tơ trạng thái ẩn của thời điểm trước làm đầu vào, và cứ tiếp tục như vậy đến khi đầu ra của RNN là _END thì kết thúc. Xem trên hình là một ví dụ cụ thể của mô hình này trong dịch máy, với đầu vào là Encoder vector và _START trải qua một loạt các time steps (thời điểm) ta sẽ có đầu ra chuỗi “O1, O2, O3, O4, O5”, nếu đúng như mong muốn thì các chuỗi này sẽ chính là “Bạn đang làm gì thế”. Để cho quá trình huấn luyện nhanh hội tụ, khi huấn luyện người ta hay sử dụng một kỹ thuật là “Teacher Forcing”, trong đó tại các thời điểm thì đầu vào của RNN sử dụng chính các đầu ra thực tế của thời điểm trước thay vì sử dụng đầu ra dự đoán được. Trên hình 5, các đường nét đứt chính là biểu diễn của việc sử dụng các đầu ra thực tế của thời điểm trước làm đầu vào cho RNN chứ không dùng các đầu ra dự đoán ở các đường nét liền, cụ thể khi huấn luyện tại thời điểm thứ 2 ta sử dụng “Bạn” làm đầu vào cho RNN chứ không phải là “O1”.
  
  Mô hình Sequence to Sequence dựa trên Auto Encoder tuy đã giải quyết bài toán chuyển hóa chuỗi đầu vào thành chuỗi đầu ra có độ dài khác nhau, tuy nhiên nó tồn tại rất nhiều hạn chế. Dễ thấy nhất đó là việc sử dụng mạng RNN Encoder duyệt qua từng phần từ của chuỗi đầu vào và rồi lấy ra vector trạng thái ẩn của mạng này ở thời điểm cuối cùng, và hi vọng rằng nó sẽ nhớ hết những thông tin cần thiết của chuỗi đầu vào trước khi chuyển hóa thành chuỗi đầu ra, điều này thật ngây thơ. Với những chuỗi dài, sau khi duyệt qua hàng loạt các phần thì thông tin ở những phần đầu sẽ bị “quên”, và đôi khi lại nhớ những thứ không cần nhớ. Do đó “Attention” sinh ra chính là để giải quyết những nhược điểm này.
 
 ### CƠ CHẾ CỦA ATTENTION TRONG MÔ HÌNH
  với ý tưởng sử dụng một vector bối cảnh có thể tương tác với toàn bộ vector trạng thái ẩn của encoder thay vì chỉ sử dụng vector trạng thái ẩn cuối cùng để tạo ra vector biểu diễn cho decoder. Cụ thể hơn, mô hình seq2seq khi áp dụng cơ chế attention vào sẽ có cấu trúc như sau:
  
  Chi tiết các bước, tại mỗi time-step t ở phía decoder:
  
  **Bước 1**: Nhận vector trạng thái ẩn của decoder <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" /> và tất cả các vector trạng thái ẩn của encoder <img src="https://latex.codecogs.com/svg.image?h_{s}" title="https://latex.codecogs.com/svg.image?h_{s}" />
 
  **Bước 2**: Tính điểm attention. Với mỗi vector trạng thái ẩn của encoder thì ta cần tính điểm thể hiện sự liên quan với vector trạng thái ẩn <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" /> của decoder. ụ thể, ta sẽ áp dụng một phương trình tính điểm "attention" với đầu vào là vector trạng thái ẩn decoder - <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" />  và một vector trạng thái ẩn của encoder - <img src="https://latex.codecogs.com/svg.image?h_{s}" title="https://latex.codecogs.com/svg.image?h_{s}" /> và trả về một giá trị vô hướng  <img src="https://latex.codecogs.com/svg.image?score&space;(h_{t},\overline{h}_{s})" title="https://latex.codecogs.com/svg.image?score (h_{t},\overline{h}_{s})" />
  
  **Bước 3**: Tính trọng số attention. Áp dụng hàm softmax với đầu vào là điểm attention
  
  <img src="https://latex.codecogs.com/svg.image?\alpha&space;_{ts}&space;=&space;\frac{e^{score(h_{t},\overline{h}_{s})}}{e^{\sum_{s'=1'}^{S}score(h_{t},\overline{h}_{s})}}&space;" title="https://latex.codecogs.com/svg.image?\alpha _{ts} = \frac{e^{score(h_{t},\overline{h}_{s})}}{e^{\sum_{s'=1'}^{S}score(h_{t},\overline{h}_{s})}} " />
  
   **Bước 4**: Tính toán vector bối cảnh <img src="https://latex.codecogs.com/svg.image?c_{t}&space;" title="https://latex.codecogs.com/svg.image?c_{t} " /> là tổng của các trọng số attention nhân với vector trạng thái ẩn của decoder tại time-step tương ứng:
   
   <img src="https://latex.codecogs.com/svg.image?c_{t}&space;=&space;\sum_{s'&space;=&space;1'}^{S}&space;\alpha_{ts}\overline{h'}_{s}&space;" title="https://latex.codecogs.com/svg.image?c_{t} = \sum_{s' = 1'}^{S} \alpha_{ts}\overline{h'}_{s} " />
   
   Cuối cùng, các vector attention <img src="https://latex.codecogs.com/svg.image?a_{t}" title="https://latex.codecogs.com/svg.image?a_{t}" /> dùng để đưa ra đầu ra được tính dựa trên vector bối cảnh <img src="https://latex.codecogs.com/svg.image?c_{t}" title="https://latex.codecogs.com/svg.image?c_{t}" /> và vector trạng thái ẩn ở decoder <img src="https://latex.codecogs.com/svg.image?h_{t}" title="https://latex.codecogs.com/svg.image?h_{t}" />

### CODE MINH HỌA
   
 
