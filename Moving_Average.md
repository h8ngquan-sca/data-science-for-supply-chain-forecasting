# 1. Moving Average

Đầu tiên, chúng ta sẽ tiếp cận mô hình đầu tiên và cũng là mô hình đơn giản nhất, sau đó sẽ di chuyển dần sang các mô hình phức tạp hơn.

Chương này sẽ gồm 2 phần chính:

## 1.1. Mô hình Trung bình động

Mô hình Trung bình động dựa trên ý kiến cho rằng nhu cầu tương lai sẽ tương đồng với quan sát nhu cầu gần đây.

Mô hình giả định rằng dự báo chính là trung bình cộng nhu cầu của n kỳ gần nhất

### Công thức:

```
f(t) = (1/n) × Σ(d(t-i)) từ i=1 đến n
```

Trong đó:
- `f(t)` = dự báo tại thời điểm t
- `n` = số kỳ quan sát
- `d(t-i)` = nhu cầu tại các thời điểm trước đó
- `Σ` = tổng cộng

### Dự báo tương lai

Khi đã hết dữ liệu lịch sử, mô hình xác định dự báo tương lai chính là dự báo cuối cùng (gần nhất) dựa trên dữ liệu lịch sử. Điều này có nghĩa là, với mô hình Trung bình động, dự báo nhu cầu tương lai sẽ phẳng đều (1 đường thẳng). Do đó, có thể kết luận rằng mô hình Trung bình động không có khả năng nhận diện yếu tố Xu hướng (Trend)

### Ký hiệu:

- **Nhu cầu** - Demand ký hiệu là `d`
- **Dự báo** - Forecast ký hiệu là `f`
- Khi muốn biểu diễn dự báo (hoặc nhu cầu) tại thời điểm t, ta ký hiệu là `f_t` (hoặc `d_t`)
- `f_t` là dự báo của thời gian t
- `n` là số kỳ quan sát sử dụng để tính trung bình cộng
- `d_t` là nhu cầu trong thời gian t
- `d_0` là nhu cầu tại mốc thời gian 0 (đầu tháng, đầu tuần...)
- `f_0` là dự báo cho nhu cầu tại mốc thời gian 0

## 1.2. Đánh giá

### Mô hình Naive Forecast

Dựa trên hình 1.1, ta thấy khi mô hình Trung bình động có n=1 thì dự báo của hôm nay chính là nhu cầu thực tế của ngày hôm qua. Đây là mô hình **Naive Forecast**.

Mô hình Naive Forecast là mô hình dự báo đơn giản nhất luôn dự báo cho kỳ tiếp theo chính bằng nhu cầu thực tế của kỳ gần nhất vừa quan sát được. Mô hình sẽ phản ứng rất nhanh với bất kỳ biến động nào của nhu cầu, nhưng ngược lại, mô hình sẽ rất nhạy cảm với những dữ liệu Noise và Ngoại lai (Outliers).

**Noise** được định nghĩa là sự biến động không thể giải thích của dữ liệu.

### Sự đánh đổi (Trade-off)

Để phòng tránh tác động của Noise và Outliers chúng ta có thể tăng số kỳ quan sát (n>1) như n=8 trong hình 1.1, đổi lại mô hình sẽ phản ứng chậm hơn với sự biến động của nhu cầu thực tế nhưng mô hình sẽ ổn định hơn mô hình Naive.

Chúng ta phải thực hiện sự đánh đổi (trade-off) giữa sự phản ứng (reactivity) và sự ổn định (smoothness):

- **n nhỏ**: Mô hình phản ứng nhanh với sự thay đổi của nhu cầu, nhưng lại rất nhạy cảm với "nhiễu" (biến động ngẫu nhiên).

- **n lớn**: Dự báo sẽ mượt mà và ổn định hơn (loại bỏ được nhiễu), nhưng lại phản ứng rất chậm chạp khi xu hướng thị trường thay đổi.

### Nhược điểm

1. **No Trend** - Mô hình hoàn toàn không nhận diện được Xu hướng, do đó dự báo tương lai sẽ luôn là một đường thẳng nằm ngang

2. **No Seasonality** - Mô hình không có tính Mùa vụ, do đó không nắm bắt được các chu kỳ lặp lại của nhu cầu

3. **Flat Historical Weighting** - Đây là điểm yếu lớn về mặt toán học, bởi vì mô hình coi dữ liệu của các kỳ quan sát cũ quan trọng ngang với dữ liệu mới nhất vừa xảy ra (thực tế dữ liệu mới nhất thương mang nhiều thông tin giá trị hơn)
