# Tiếp tục chinh phục từng lab tại CyberDefenders: SOC Level 1 - Oski Lab

*Mô tả: Kế toán tại công ty đã nhận được một email có tiêu đề "Lệnh mới khẩn cấp" từ một khách hàng vào cuối buổi chiều. Khi anh ta cố gắng truy cập hóa đơn đính kèm, anh ta phát hiện ra nó chứa thông tin đặt hàng sai. Sau đó, giải pháp SIEM đã tạo ra một cảnh báo liên quan đến việc tải xuống một tệp độc hại có khả năng. Sau khi điều tra ban đầu, người ta thấy rằng tệp PPT có thể chịu trách nhiệm cho việc tải xuống này. Bạn có thể vui lòng tiến hành kiểm tra chi tiết về tệp này?*

## Ở lab này trước tiên được cung cấp một file hash.txt. Yêu cầu sử dụng nền tảng VR và Hybrid Analysis để điều tra
![Ảnh ban đầu](./images/0.1.png)

### Câu 1: Xác định thời gian tạo của phần mềm độc hại có thể cung cấp cái nhìn sâu sắc về nguồn gốc của nó. Thời điểm tạo phần mềm độc hại là gì?

> Trước tiên mang MD5 hash lên Virus total để xem có những thông tin hữu ích gì cho chúng ta. Để lấy được thời gian tạo của tệp mã độc thì ta vào phần Detail sẽ thấy kết quả phù hợp.
![Thời gian tạo](./images/1.1.png)
> Kết quả thu được: 2022-09-28 17:40

### Câu 2: Xác định máy chủ lệnh và điều khiển (C2) mà phần mềm độc hại giao tiếp có thể giúp truy tìm trở lại kẻ tấn công. Máy chủ C2 nào làm phần mềm độc hại trong tệp PPT giao tiếp với?

> Để trả lời câu này vào tab Behavior của tệp Virus total vừa tìm hiểu xem có điều gì thú vị không.

> Xác định được IP máy nạn nhân bị tấn công là **171.22.28.221**. Sau đó tìm các giao thức truy cập như TCP, HTTP...

> Nhưng trong trường hợp này chú ý vào HTTP request với phương thức POST để kiểm tra kết quả có phù hợp với pattern đáp án không

![Điều tra file c2](./images/2.1.png)

>Kết quả đúng là: http://171.22.28.221/5c06c05b7b34e8e6.php