Bước 1: Chuẩn bị dataset và file data.yaml
- Dataset có 18681 ảnh dùng cho việc train và 1004 ảnh cho validation. Để setup cho việc huấn luyện mô hình, trước tiên ta sẽ lên trang web Kaggle. Upload notebook trong train_code và chọn mục add input Upload -> New Dataset. Tiến hành tải dataset lên. Đặt tên cho thư mục mẹ chứa dataset là dataset-yolo11n.
- Để mô hình có thể nhận biết được số class và đường dẫn tới file dataset, ta sẽ tạo một file data.yaml nằm trong thư mục mẹ tên configuration trên Kaggle. File data.yaml sẽ nằm trong thư mục train_code.

Bước 2: Thiết lập cần thiết và huấn luyện mô hình
- Trong Kaggle, chọn Accelerator là GPU P100. 
- Sau đó chạy lệnh !pip instrall ultralytics để cài đặt các thư viện cần thiết.
- Để huấn luyện mô hình, chạy lệnh !yolo detect train data=/kaggle/input/configuration/data.yaml model=yolo11n.pt epochs=70 imgsz=320 project=/kaggle/working name=runs.

Bước 3: Đánh giá mô hình
Trên Colab
- Tải toàn bộ dataset lên google drive.
- Đặt tên dataset gốc là data.zip và dataset gồm 200 ảnh là rsud20k.zip.
- Thực hiện việc copy thư mục từ drive qua Colab như trong notebook. Sau khi đã copy xong tiến hành giải nén và đặt tên thư mục giải nén cho dataset gốc là full_dataset và dataset 200 ảnh là test_dataset.
- Chỉnh sử lại đường dẫn cho file data.yaml là đường dẫn tới tập val của từng loại dataset.
- Cuối cùng chạy lệnh !yolo val model=/content/best_float32.tflite data=/content/data.yaml imgsz=320 để thực hiện đánh giá mô hình trên tập dữ liệu mong muốn.
Trên Kaggle
- Sau khi đã có file best.pt ở thư mục /kaggle/working/runs, ta tiến hành tải model về và chọn Upload -> New model, đặt tên cho thư mục mẹ chứa best.pt là best-model và chạy lệnh sau để đánh giá model trên tập val: !yolo val model=/kaggle/input/best-model/pytorch/default/1/best.pt data=/kaggle/input/configuration/data.yaml imgsz=320.
- Đánh giá trên tập test (RSUD20K): Chỉ cần sửa lại đường dẫn trong file data.yaml thành val: images/test và chạy lệnh sau để đánh giá mô hình !yolo val model=/kaggle/input/best-model/pytorch/default/1/best.pt data=/kaggle/input/configuration/data.yaml imgsz=320.
- Cuối cùng là đánh giá mô hình trên tập test của thầy: Tiến hành upload dataset gồm 200 ảnh lên Kaggle và đặt tên thư mục mẹ chứa 200 ảnh là dataset-test. Sửa lại file data.yaml từ path: /kaggle/input/dataset-yolo11n/rsud20k thành path: /kaggle/input/dataset-test/rsud20k và giữ nguyên val: /images/test. Sau đó chạy lệnh sau: !yolo val model=/kaggle/input/best-model/pytorch/default/1/best.pt data=/kaggle/input/configuration/data.yaml imgsz=320.

Bước 4: Convert mô hình sang định dạng tflite
- Tạo notebook mới hoặc tải notebook hiện tại lên Google Colab. Sau đó tải best.pt lên Google Colab.
- Chỉ cần chạy lệnh !yolo export model=/content/best.pt format=tflite imgsz=320 để export, kết quả sẽ cho ra mô hình best_float32.tflite. 

