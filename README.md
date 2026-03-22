# Final

## Đánh giá notebook `CPV_MLBase_baseline.ipynb`
- Pipeline: EdgeBoxes đề xuất vùng + đặc trưng HOG kết hợp histogram màu HSV + Linear SVM (có 1 vòng hard-negative mining).
- Dataset YOLO: 7 lớp (`Backpack`, `Book`, `Bottle`, `Cup`, `Laptop`, `Phone`, `Wallet`) với 3,665 ảnh train, 488 validation và 189 test.
- Đặc trưng:
  - Vector 420 chiều.
  - Tập train được cân bằng lại: nền bị giới hạn ≤3× số mẫu dương mỗi ảnh, áp dụng lật ngang ngẫu nhiên để tăng mẫu dương; trọng số lớp được tính động.
- Đánh giá trên tập test:
  - mAP@0.5 = **0.00**
  - mAP@0.5:0.95 (COCO) = **0.00**
  - Tổng 118 dự đoán: IoU trung bình 0.1916, trung vị 0.1153, chỉ 11/118 dự đoán (9.32%) đạt IoU ≥ 0.5.
- Nhận xét:
  - Mô hình gần như không phát hiện được đối tượng (mAP = 0).
  - Nguyên nhân khả dĩ: đặc trưng đơn giản, mất cân bằng mẫu, cảnh báo NumPy “Conversion of an array with ndim > 0 to a scalar” khi tính đặc trưng/IoU (đã chuẩn hóa lại cast kiểu và giới hạn nền để giảm tác động; cần chạy lại notebook để cập nhật số liệu sau khi sửa).
  - Xử lý mất cân bằng: giới hạn negative ≤3× positive/ảnh, tăng cường lật ngang ngẫu nhiên, trọng số lớp động (class_weight + sample_weight khi huấn luyện SVM).
  - Hướng cải thiện: mô hình mạnh hơn (ví dụ backbone học sâu) và/hoặc cải thiện bước tạo nhãn huấn luyện; khắc phục triệt để cảnh báo NumPy nêu trên khi tái huấn luyện.
  - Kết quả được ghi nhận như baseline hiện tại để làm mốc so sánh cho các lần cải thiện tiếp theo (không phải kết quả cuối cùng mong muốn).
