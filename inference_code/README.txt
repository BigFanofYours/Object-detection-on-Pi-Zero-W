Bước 1: Kết nối Pi và laptop
Thực hiện SSH cho Pi bằng laptop cá nhân theo đúng như chỉ dẫn của lab3: Kết nối Pi với màn hình và bàn phím -> Laptop và Pi đăng nhập vào cùng một mạng không dây -> SSH trên laptop để kết nối với Pi.

Bước 2: Tải file lên Pi
- Sau khi đã SSH xong, tải phần mềm FileZilla để thực hiện việc chuyển dữ liệu.
- Kết nối với địa chỉ IP của Pi, username là Pi, mật khẩu là 1q2w3e4r và sử dụng port 22.
- Thực hiện việc tải 200 ảnh và 5 file main.py, model.py, metrics.py, nms.py và best_float32.tflite lên Pi. Trong đó, 200 ảnh và label sẽ được để trong thư mục mẹ là anh_test, anh_test này sẽ cùng chung thư mục với 5 file còn lại.

Bước 3: Thực thi mô hình
- Thực hiện lệnh "sudo opencv-python" để cài đặt thư viện opencv.
- Trên laptop cá nhân, cd tới thư mục chứa tất cả các file này, chạy lệnh "python main.py" là hoàn thành.