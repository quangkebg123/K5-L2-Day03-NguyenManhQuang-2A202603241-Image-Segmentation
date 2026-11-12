# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp:2A202603241
- Ngày / CVAT local:12 / CVAT online
- Công cụ đã dùng: CVAT online

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task            | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --------------- | ----------------- | -----------------: | ---------------------------: |
| easy_semantic   | easy_semantic     |              3 / 3 |                           20 |
| medium_instance | medium_instance   |              3 / 3 |                           32 |
| hard_panoptic   | hard_panoptic     |              2 / 2 |                           30 |
| cp1_holes       | cp1_holes         |              1 / 1 |                            3 |
| cp2_slice       | cp2_slice         |              1 / 1 |                            3 |
| cp5_occlusion   | cp5_occlusion     |              1 / 1 |                            3 |
| cp3_thin        | cp3_thin          |              1 / 1 |                            3 |
| cp4_curb        | cp4_curb          |              1 / 1 |                            3 |
| cp6_coverage    | cp6_coverage      |              1 / 1 |                            3 |
| **Tổng tối đa** |                   |                    |                      **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 000000181542.jpg , vị trí person 17
- Class và quy tắc tôi dùng để chọn biên: class `person`; bám theo đường viền cơ thể nhìn thấy, không lấy pixel xe hoặc nền vào mask và không tự vẽ tiếp phần bị vật khác che.
- Nếu dùng gợi ý sau đó: không dùng gợi ý tự động.
- Quyết định gán nhãn: tôi tự vẽ object này trước khi xem gợi ý; chỉ gán phần người nhìn thấy theo class `person`.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic/000000460147.jpg/car nhỏ sau ảnh
- Lỗi thuộc loại: quá nhỏ để để instance từng car
- Bằng chứng tôi nhìn thấy: car nhỏ li ti sát nhau liền kề
- Quy tắc và hành động sửa: mask toàn bộ car nhỏ vào 1 class
- Sau sửa đã Save và export lại chưa? chưa thể xác nhận. lỗi này e chưa sửa

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Tôi chưa nhớ chắc ba ca mình đã cân nhắc lúc làm bài. Các dòng dưới đây là ba điểm cụ thể cần đối chiếu với mask đã vẽ và hỏi coach nếu còn phân vân; đây không phải khẳng định rằng tôi đã gặp hoặc sửa lỗi ở các vùng này.

| Ảnh/vị trí                                                          | Hai cách hiểu có thể                                                      | Quy tắc/chứng cứ                                                                                                     | Quyết định hoặc câu hỏi cho coach                                           |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| cp1_holes / `000000144300.jpg`, các khe ở khung và bánh xe mô tô    | Khe nhìn xuyên qua khung xe là nền cần khoét, hay giữ liền trong mask xe? | Theo quy tắc checkpoint, kính/khe/chi tiết nằm trong mask; không khoét lỗ nền nếu task yêu cầu giữ chúng trong mask. | Coach xác nhận giúp cách xử lý các khoảng trống của khung xe trong bài này. |
| cp2_slice / `000000017627.jpg`, cụm xe sát nhau giữa ảnh            | Hai xe chạm/che nhau là một vật thể hay hai instance cùng class?          | Dùng đường viền riêng của từng xe; hai xe cùng class vẫn là hai instance.                                            | Coach xác nhận giúp ranh tách giữa các xe ở cụm giữa ảnh.                   |
| cp4_curb / `7d83710e-4697c3b2.jpg`, bó vỉa cạnh mặt đường và vỉa hè | Ranh road–sidewalk theo chỗ đổi màu hay theo bó vỉa/chức năng?            | Dựa vào bó vỉa và chức năng; không quyết định chỉ theo màu.                                                          | Coach xác nhận giúp vị trí ranh tại đoạn bó vỉa cong cạnh gốc cây.          |
