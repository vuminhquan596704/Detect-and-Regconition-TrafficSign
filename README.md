# ĐỀ CƯƠNG 
https://docs.google.com/document/d/1wiFmysAprkLWbK6pKzVj8bDaiRU14u0t/edit?usp=sharing&ouid=104188203148634091558&rtpof=true&sd=true
# YOLO Object Detection
In the previous section, we presented the structure of YOLO, and in this section, we will discuss how the YOLO algorithm works for detecting and recognizing traffic signs.
The YOLO algorithm works based on the following steps:

**Residual Blocks**: 
Để phát hiện và nhận biết biển báo giao thông một cách dễ dàng, thuật toán YOLO chia hình ảnh đầu vào thành một lưới NxN với các ô có kích thước bằng nhau, trong đó N trong trường hợp của chúng tôi là 4 như trong hình bên phải. Mỗi ô trong lưới biểu thị việc định vị và dự đoán lớp đối tượng nằm trong ô cùng với xác suất của từng đối tượng được dự đoán.

![Ảnh chụp màn hình 2024-05-14 181929](https://github.com/nguyentiendat12032003/NCKH_Traffic_Detect_Adruinocar/assets/111034777/6f862e32-37c8-41a2-ba90-a01d07a1fe49)

**Bounding Box Regression**:
Giai đoạn tiếp theo liên quan đến việc xác định các hộp giới hạn phác thảo tất cả các đối tượng trong ảnh. Số lượng hộp giới hạn có thể khớp với số lượng đối tượng có trong ảnh.
YOLO sử dụng một mô-đun hồi quy duy nhất để xác định các thuộc tính của các hộp giới hạn này, được biểu thị bằng Y theo định dạng sau Y = [pc, bx, by, bh, bw, c1, c2]
Quá trình này đặc biệt quan trọng trong giai đoạn đào tạo của mô hình.
Phần tử pc biểu thị điểm xác suất của lưới chứa một đối tượng. Ví dụ: tất cả các lưới được đánh dấu màu đỏ sẽ có điểm xác suất lớn hơn 0 (có ý nghĩa). Hình ảnh bên phải là phiên bản đơn giản hóa, vì xác suất của mỗi ô màu vàng bằng 0 (không đáng kể).

![Ảnh chụp màn hình 2024-05-14 182046](https://github.com/nguyentiendat12032003/NCKH_Traffic_Detect_Adruinocar/assets/111034777/060393a0-22f1-45a6-ba29-d73b4a3340e6)

**Intersection Over Unions or IOU for short**:
Các thuật toán phát hiện đối tượng có thể được chia thành hai loại chính: máy dò một lần và máy dò hai giai đoạn. YOLO là máy dò một lần sử dụng mạng thần kinh tích chập hoàn toàn để xử lý hình ảnh. Mục tiêu của IOU (giá trị từ 0 đến 1) là loại bỏ các hộp lưới như vậy để chỉ giữ lại những hộp có liên quan. Đây là logic đằng sau nó:
Người dùng xác định ngưỡng lựa chọn IOU của mình, ví dụ: có thể là 0,5.
Sau đó, YOLO tính toán IOU của mỗi ô lưới là Vùng giao nhau chia cho Vùng liên minh.
Cuối cùng, nó bỏ qua dự đoán về các ô lưới có IOU ≤ threshold và xem xét những ô có IOU > threshold.
**Non - Maximum Suppression**:
Chỉ thiết lập ngưỡng cho Giao lộ trên Liên minh (IOU) không phải lúc nào cũng đủ vì một đối tượng có thể tạo ra nhiều hộp có IOU vượt quá ngưỡng. Việc giữ lại tất cả các hộp như vậy có thể gây ra tiếng ồn. Đây là lúc tính năng Ngăn chặn không tối đa (NMS) phát huy tác dụng, cho phép chúng tôi chỉ giữ lại các hộp có điểm xác suất phát hiện cao nhất.
# Kết quả huấn luyện - Thực nghiệm 
**Tập dữ liệu**: https://app.roboflow.com/ds/GgJMqMOCK5?key=YeAtuMNV0M

**Độ chính xác của mô hình là 86.8%**

Precision - Recall Curve của từng lớp 

![Ảnh chụp màn hình 2024-05-14 182358](https://github.com/nguyentiendat12032003/NCKH_Traffic_Detect_Adruinocar/assets/111034777/a4250110-fdfd-474f-9a27-58324deeacb4)

Confusion Matrix khi test mô hình trên tập dữ liệu test

![Ảnh chụp màn hình 2024-05-14 182727](https://github.com/nguyentiendat12032003/NCKH_Traffic_Detect_Adruinocar/assets/111034777/78d4efa9-6bcc-4693-9d95-a6f5c6a2f7aa)

**Thực nghiệm phát hiện và nhận dạng biển báo giao thông trên ảnh**

![Hình ảnh Hình ảnh Hình ảnh Hình ảnh Hình ảnh Hình ảnh](https://github.com/nguyentiendat12032003/NCKH_Traffic_Detect_Adruinocar/assets/111034777/1854479f-02f6-4527-938d-620779e3f2cd)
