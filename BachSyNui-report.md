# Báo cáo cá nhân — Ngày 11
Họ tên: Bạch Sỹ Núi               Mã học viên: 2A202603267  
Phiên bản CVAT (Help → About): v2.82.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2  
Thời điểm export (ngày giờ trên CVAT): 20/11/2026 23:31 UTC+7    Số lần nộp lại sau Rework: 1  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane (polyline), road_curb (polyline), crosswalk (polygon), drivable (polygon), traffic_light (rectangle), traffic_sign (rectangle) |
| Thuộc tính và giá trị | Đúng | Đủ thuộc tính select và checkbox theo taxonomy |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source |
Cách kết thúc polyline trên bản CVAT này: Bấm phím `N` sau khi click xong điểm cuối cùng.  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ Tag trên thanh công cụ bên trái, chọn label tag, sau đó mở Details trong tab Objects để kiểm tra và sửa thuộc tính `value`.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 34 | 7 | 9 | 27 | 42 | 29 |
| front-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 11 | 5 | 10 | 1 | 4 | 3 |
| fisheye-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | `lane` | Cố vẽ L1/R1 theo vết mờ hay không vẽ | Không vẽ | Mặt đường không có vạch sơn rõ ràng; guideline quy định không vẽ vạch mà ảnh không thấy (QC1-02 được miễn) |
| A08 | `lane` | Vạch phân cách tim đường là vạch đơn hay vạch đôi | `single` / `double` | Quan sát kỹ đoạn có vạch đôi song song thì chọn `kind=double` nhưng chỉ vẽ 1 polyline ở tâm vệt |
| B06 | `lane` | position L1/R1 hay other | `other` | Camera góc sườn trái (`MVL`), guideline mục 4 yêu cầu camera hai bên luôn đặt `position = other` |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Xuân Anh (MSV: 2A202603160)  Quyết định nhận được: Rework (lần 1)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 | 3 | Đồng ý | Đã sửa: Đổi toàn bộ lane trên camera hai bên sườn (B06, B07, B08) thành position=other |
| QC1-02 | 2 | Đồng ý | Đã kiểm tra lại A07, A09 và bổ sung vạch còn thiếu |

*Ghi chú sau Rework*: Bản cũ đã được lưu trữ trong thư mục `r1/`. Bản sửa mới được export thành công, chạy `road_check lint` không còn lỗi nặng nào (lỗi nặng giảm từ 13 xuống còn 3 ở các ca miễn trừ A05, A06), manifest được tạo mới với `--revision 2`.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `BachSyNui-front.zip` | Có (`road_check lint` đạt) | 9 / 9 | 8 / 8 | Có (`camera = front`) |
| `BachSyNui-fisheye.zip` | Có (`road_check lint` đạt) | 3 / 3 | 2 / 2 | Có (`camera = fisheye_*`) |

## 6. Ảnh chụp màn hình
*(Các ảnh chụp màn hình minh chứng quá trình làm trên CVAT)*:
1. Tab Labels của project: Đã kiểm tra đủ 6 label hình và 4 label tag.
2. Một ảnh camera trước đã gán đủ (A01/A03): Đầy đủ lane L1/R1, vùng drivable direct/alternative, đèn và biển báo.
3. Một ảnh fisheye đã gán (B01/B06): Polyline uốn lượn cong theo cung của thấu kính fisheye, không gán thân xe mình.
4. Một đoạn XML export có `<polyline label="lane">` và các thẻ `<attribute>`.

## 7. Tự đánh giá
* **Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20**:  
  Lỗi mắc nhiều nhất ở lần nộp 1 là **QC1-03 (sai thuộc tính position ở camera sườn fisheye)** do CVAT tự động điền giá trị mặc định là `L1`. Cách tránh ở Ngày 20: Luôn tạo checklist self-QC sau khi vẽ xong mỗi ảnh, mở bảng Details để rà soát toàn bộ các thuộc tính (`position`, `color`, `style`, `kind`) trước khi chuyển ảnh.
* **Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào**:  
  Nhãn `lane` đi vào module Lane Detection / LKA (Lane Keeping Assist). Nếu vạch sơn ở camera sườn xe (`MVL`/`MVR`) bị gán nhầm là `L1` (vạch bên trái làn xe đang chạy thẳng), mô hình sẽ học sai rằng xe đang chạy lệch làn hoặc hiểu nhầm không gian phía hông là làn đường chính phía trước, dẫn đến việc hệ thống tự lái ra quyết định đánh lái đột ngột gây mất an toàn giao thông nghiêm trọng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 520 | 545 | 570 | 592 | 610 |
| x của bạn kia | 518 | 544 | 571 | 590 | 608 |

Trả lời 3 câu:
1. **Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?**  
   Hàng `y = 560` (hoặc hàng xa nhất tương ứng với phần bị dừng sớm) sẽ không có điểm giao cắt nội suy, dẫn đến model dự đoán nhầm là vạch kết thúc sớm và phân loại hàng đó thành "không có làn".
2. **So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?**  
   Ở hàng 720 lệch 2 px, ở hàng 560 lệch 2 px. Lệch ở hàng 720 (sát đầu xe / đáy ảnh) ảnh hưởng tới hệ thống LKA nhiều hơn, vì các điểm sát xe quyết định trực tiếp đến góc lệch làn hiện thời (lateral deviation) và lệnh điều khiển vô lăng tức thì của xe.
3. **Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?**  
   Cách tính tọa độ x trên từng hàng y về mặt hình học thuần túy không đổi, nhưng thứ tự lưu các điểm trong XML bị đảo ngược. Các script nội suy một chiều, script kiểm tra hướng di chuyển của xe (chiều tiến) hoặc các thuật toán bám vạch từ gần ra xa (tracking / curve fitting) sẽ gặp lỗi hoặc phải tốn thêm bước tiền xử lý đảo ngược danh sách điểm.
