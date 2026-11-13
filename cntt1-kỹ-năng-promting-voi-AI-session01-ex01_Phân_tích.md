


## Bước 1 : Thiết kế 2 phương án prompt

### Phương án 1: Zero-shot (chỉ nêu luật, không ví dụ)

```
- TÍCH CỰC: khách khen sản phẩm ngon, giá rẻ, chất lượng tốt. 
- TIÊU CỰC: khách chê giao hàng chậm, thái độ nhân viên tệ, sản phẩm không đạt. 
- CẦN HỖ TRỢ: khách hỏi thông tin (địa chỉ cửa hàng, giá, giờ mở cửa, cách đặt hàng).
```

### Phương án 2: Few-shot (kèm 3 ví dụ mẫu, có câu mỉa mai)

```
1. "Phở ngon quá, giá lại rẻ, ủng hộ lâu dài!"  TÍCH CỰC

2. "Giao hàng chậm chết được, nhân viên còn càu nhàu."  TIÊU CỰC

3. "Quán phục vụ chu đáo quá, bắt khách đợi hẳn 1 tiếng!"  TIÊU CỰC

4. "Cho em hỏi địa chỉ cửa hàng ở Q1 ở đâu ạ?" → CẦN HỖ TRỢ 
```

----------

## Bước 2  Bảng so sánh Trade-off

|Tiêu chí|Giải pháp 1 (Zero-shot)|Giải pháp 2 (Few-shot)|
|-|-|-|
|Độ dễ hiểu|Cao, |viết nhanh\Trung bình, cần soạn ví dụ|
|Tốn token|Ít|Nhiều hơn (do ví dụ)|
|Xử lý |Kém |Tốt|
|Độ chính xác chung|Trung bình|Cao hơn
|Chi phí vận hành|Thấp|Cao hơn một chút|

## Bước 3 : Test 



**Kết luận:** Few-shot chính xác hơn rõ rệt ở các câu có sắc thái / mỉa mai, vì ví dụ mẫu "dạy" AI nhận diện cấu trúc ẩn mà chỉ viết luật không thể bao quát. Đánh đổi: tốn thêm token và phải bảo trì bộ ví dụ.

