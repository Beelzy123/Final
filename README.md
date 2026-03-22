# Final

## Đánh giá notebook `CPV_MLBase_need_fix.ipynb`
- Pipeline: EdgeBoxes đề xuất vùng + đặc trưng HOG kết hợp histogram màu HSV + Linear SVM (có 1 vòng hard-negative mining).
- Dataset YOLO: 7 lớp (`Backpack`, `Book`, `Bottle`, `Cup`, `Laptop`, `Phone`, `Wallet`) với 3,665 ảnh train, 488 val và 189 test.
- Đặc trưng: vector 420 chiều; tập train ban đầu có 61,753 mẫu (phần lớn là nền `-1`, tiếp theo là lớp Laptop với 6,636 mẫu; các lớp khác ~100–2,400 mẫu).
- Đánh giá trên tập test:
  - mAP@0.5 = **0.00**
  - mAP@0.5:0.95 (COCO) = **0.00**
  - Tổng 118 dự đoán: IoU trung bình 0.1916, trung vị 0.1153, chỉ ~9.3% dự đoán đạt IoU ≥ 0.5.
- Nhận xét:
  - Mô hình gần như không phát hiện được đối tượng (mAP = 0).
  - Nguyên nhân khả dĩ: đặc trưng đơn giản, mất cân bằng mẫu, cảnh báo trích xuất đặc trưng/NumPy; cần mô hình mạnh hơn (ví dụ backbone học sâu) hoặc cải thiện bước tạo nhãn huấn luyện.
  - Kết quả được ghi nhận như baseline hiện tại để làm mốc so sánh cho các lần cải thiện tiếp theo (không phải kết quả cuối cùng mong muốn).
