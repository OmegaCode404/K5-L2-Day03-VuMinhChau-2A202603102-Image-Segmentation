# Báo cáo thực hành Day 3

- Mã học viên theo lớp: 2A202603102
- Ngày: 12/11/2026
- Công cụ: Mask2Former Swin-Small COCO Panoptic qua `scripts/auto_label_hard_panoptic.py` (CPU); kiểm tra cấu trúc ZIP bằng `scripts/inspect_submissions.py`.

## 1. Bài đã nộp

Số ảnh/mask dưới đây được đếm từ ZIP, không xác nhận đã được rà soát hoặc Save trong CVAT. `hard_panoptic` và các checkpoint là gợi ý tự động, cần kiểm tra trước khi dùng.

| Task | File ZIP | Nội dung nhận diện được | Điểm tối đa |
| --- | --- | --- | ---: |
| easy_semantic | easy_semantic.zip | 3 semantic masks; cấu trúc OK | 20 |
| medium_instance | medium_instance.zip | Không nhận diện được COCO JSON hoặc ảnh; lỗi cấu trúc | 32 |
| hard_panoptic | hard_panoptic.zip | 2 ảnh, 44 masks; cấu trúc OK, cần rà soát trực quan | 30 |
| cp1_holes | cp1_holes.zip | 1 ảnh, 5 masks; cấu trúc OK | 3 |
| cp2_slice | cp2_slice.zip | 1 ảnh, 11 masks; cấu trúc OK | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 ảnh, 23 masks; cấu trúc OK | 3 |
| cp3_thin | cp3_thin.zip | 1 semantic mask; mô hình dự đoán `road`, `sky` | 3 |
| cp4_curb | cp4_curb.zip | 1 semantic mask; mô hình dự đoán `road`, `sidewalk` | 3 |
| cp6_coverage | cp6_coverage.zip | 1 semantic mask; mô hình dự đoán `building`, `car`, `person`, `road` | 3 |
| **Tổng tối đa** | | | **100** |

`cp3_thin` chưa có dự đoán cho `pole`, `traffic sign`; `cp6_coverage` chưa có dự đoán cho `sidewalk`, `vegetation`, `sky`. Nhãn trong mask/labelmap chỉ lấy từ `classes.json` của task. Kết quả tự chấm: chưa được cung cấp.

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh và object Medium đầu tiên tự vẽ: `000000181542.jpg`, class `person`; vị trí cụ thể chưa được ghi lại.
- Quy tắc chọn biên: dùng Polygon vẽ sát mép vật thể.
- Xử lý gợi ý sau đó: không dùng.

## 3. Lỗi trong bài và trạng thái xử lý

- Task/ZIP: `medium_instance.zip`.
- Loại lỗi: cấu trúc/định dạng export COCO.
- Bằng chứng: `scripts/inspect_submissions.py` báo cần đúng một COCO JSON trong `annotations/`; ZIP hiện không có COCO JSON hoặc ảnh được nhận diện.
- Cách xử lý cần làm: export lại task từ CVAT bằng `COCO 1.0`; không sửa cấu trúc ZIP thủ công.
- Trạng thái: chưa sửa, chưa export lại.
