# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602288
- Ngày / CVAT local: 17/09/2026
- Công cụ đã dùng: Brush, Polygon, CVAT AI (AI tools / Interactive segmentation)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, chiếc xe ô tô (`car`) màu đen ở vị trí tiền cảnh sát lề đường bên trái.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Quy tắc biên: Chỉ gán mask cho phần thân xe và bánh xe thực tế nhìn thấy chạm mặt đường, không vẽ lấn ra bóng đổ dưới gầm xe hoặc mặt đường nhựa; đồng thời dừng mask tại ranh giới bị che khuất bởi cột biển báo phía trước mà không tự suy đoán phần khuất.
- Nếu dùng gợi ý sau đó: vùng gợi ý tự động của AI có xu hướng nuốt cả phần bóng đổ tối màu dưới gầm xe và lấn sang vỉa hè; tôi đã dùng công cụ Brush/Polygon để cắt tỉa lại đường viền sát mép thân xe thật nhằm tránh over-segmentation.
- Nếu không dùng gợi ý: không dùng.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh `000000373353.jpg`, cụm xe ô tô đỗ song song sát nhau ở lề đường bên phải.
- Lỗi thuộc loại: gộp-tách và biên lấn nền.
- Bằng chứng tôi nhìn thấy: Gợi ý tự động gộp nhầm 2 xe đỗ sát nhau thành một mask duy nhất, đồng thời viền mask bị tràn lấn ra phần mặt đường xung quanh.
- Quy tắc và hành động sửa: Theo quy tắc instance segmentation, mỗi cá thể đếm được phải là một mask độc lập. Tôi đã xóa mask gộp, dùng Brush thu nhỏ kích thước để tách riêng thành 2 object (`car #1` và `car #2`) theo khe hở quan sát được giữa hai thân xe.
- Sau sửa đã Save và export lại chưa? Đã Save trên CVAT và export lại file `medium_instance.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Sau khi tách đúng 2 instance và gọt biên bóng đổ, per-class IoU và chỉ số matched IoU của class `car` được cải thiện rõ rệt, loại bỏ hoàn toàn lỗi gộp vật. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `easy_semantic` (`817bca71-00000000.jpg`) - Ranh giới đường và vỉa hè | Gộp chung vào `road` do màu sắc nhựa đường và vỉa hè tương đồng, hay tách riêng `sidewalk`. | Dựa vào công năng sử dụng và đường thẳng mép bó vỉa/chân công trình. | Chọn phân tách rõ `sidewalk` cho phần lối đi bộ sát chân tường nhà theo đúng chức năng. |
| 2. `hard_panoptic` (`000000350023.jpg`) - Tán cây đan xen tòa nhà phía xa | Gán toàn bộ cụm xa là `building` hay tách tỉ mỉ tán lá cây `vegetation`. | Quy tắc Stuff segmentation yêu cầu gán theo lớp chiếm ưu thế nhìn thấy ở tiền cảnh. | Zoom lớn và dùng Brush nhỏ viền tách các nhánh cây `vegetation` nhô lên trên nền trời và trước tòa nhà. |
| 3. `medium_instance` (`000000458325.jpg`) - Người điều khiển xe máy | Gộp chung người và xe thành 1 instance hay tách rời `person` và `motorcycle`. | Quy tắc instance yêu cầu tách biệt cá thể theo đúng taxonomy danh mục class. | Tách thành 2 mask riêng: 1 mask `person` (người + mũ bảo hiểm) và 1 mask `motorcycle` (phần xe nhìn thấy). |
