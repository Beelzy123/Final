# Final

## Đánh giá notebook `CPV_MLBase_baseline.ipynb`
- Pipeline: EdgeBoxes đề xuất vùng + đặc trưng HOG kết hợp histogram màu HSV + Linear SVM (có 1 vòng hard-negative mining).
- Dataset YOLO: 7 lớp (`Backpack`, `Book`, `Bottle`, `Cup`, `Laptop`, `Phone`, `Wallet`) với 3,665 ảnh train, 488 validation và 189 test.
- Đặc trưng:
  - Vector 420 chiều.
  - Tập train ban đầu: 61,753 mẫu (nền: 48,000 mẫu `-1`; Laptop: 6,636; các lớp còn lại: 100–2,439; ít nhất: 109 mẫu).
- Đánh giá trên tập test:
  - mAP@0.5 = **0.00**
  - mAP@0.5:0.95 (COCO) = **0.00**
  - Tổng 118 dự đoán: IoU trung bình 0.1916, trung vị 0.1153, chỉ 11/118 dự đoán (9.32%) đạt IoU ≥ 0.5.
- Nhận xét:
  - Mô hình gần như không phát hiện được đối tượng (mAP = 0).
  - Nguyên nhân khả dĩ: đặc trưng đơn giản, mất cân bằng mẫu, cảnh báo NumPy “Conversion of an array with ndim > 0 to a scalar” khi tính đặc trưng/IoU (cần sửa để tránh tính toán sai; số liệu có thể chưa phản ánh chính xác nhất).
  - Xử lý mất cân bằng: cân bằng mẫu theo lớp (sampling/augmentation) và trọng số lớp khi huấn luyện SVM.
  - Hướng cải thiện: mô hình mạnh hơn (ví dụ backbone học sâu) và/hoặc cải thiện bước tạo nhãn huấn luyện; khắc phục cảnh báo NumPy nêu trên.
  - Kết quả được ghi nhận như baseline hiện tại để làm mốc so sánh cho các lần cải thiện tiếp theo (không phải kết quả cuối cùng mong muốn).
