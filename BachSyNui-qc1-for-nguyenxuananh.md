# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Xuân Anh (MSV: 2A202603160)        Người kiểm (học viên): Bạch Sỹ Núi (MSV: 2A202603267)  
Ngày: 20/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): nguyenxuananh-front.zip, nguyenxuananh-fisheye.zip (revision 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 52  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 8 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 10 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 8 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 6 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 8 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | B06_04068_MVL.png | lane#2 | nặng | Camera sườn trái fisheye_left gán position=L1; quy tắc fisheye bắt buộc position=other |
| 2 | QC1-04 | A01_bc5fadac-fa6dd225.jpg | lane#0 | chính | Polyline vẽ ngược chiều từ xa về gần xe (quy tắc yêu cầu vẽ từ gần ra xa) |
| 3 | QC1-05 | A04_b7a8e795-0ff55db2.jpg | lane#1 | chính | Vạch đứt bị cắt rời thành 2 polyline riêng biệt thay vì 1 polyline nối liền |
| 4 | QC1-07 | A07_b41ace08-c8468690.jpg | drivable#0 | chính | Vùng drivable direct vẽ tràn lên mép vỉa hè dành cho người đi bộ (> 15 px) |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Vạch kẻ đường bị phai mờ gần như hoàn toàn, bạn không vẽ vạch L1/R1 | Coach xác nhận ca này được miễn trừ QC1-02 theo CHECKPOINTS |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 3 / 52 nhãn = 5.77 %   Lỗi nhẹ: 0   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Còn 1 lỗi nặng (QC1-03: nhầm position ở camera sườn hông fisheye) và tỉ lệ lỗi chính vượt ngưỡng 5% (5.77% > 5%), yêu cầu Rework để bạn sửa lại và nộp bản revision 2.
