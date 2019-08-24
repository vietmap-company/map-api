# Determining Result Quality

Mỗi kết quả được trả chứa một số thuộc tính khác nhau để giúp bạn lập trình xác định xem kết quả có đủ tốt cho mục đích của bạn không.


### match\_type

Trường này có trong kết quả của [/api/search](search.md).

Có ba giá trị: `exact`, `interpolated`, và `fallback`.

Kết quả tìm thấy chính xác những gì nó tin rằng bạn đang tìm kiếm, giá trị `match_type` sẽ là `exact`

Nếu Search Engine xác định bạn đang truy vấn địa chỉ đường phố và không thể tìm thấy địa chỉ chính xác đó, nhưng có thể ước tính tọa độ địa chỉ đó (nếu nó tồn tại) thông qua qua thuật toán nội suy thì `match type` sẽ là `interpolated`.

Khi kết quả không thể chính xác những gì bạn yêu cầu, `Search Engine` sẽ cố gắng trả lại một cái gì đó liên quan đến truy vấn của bạn một cách thông minh.

### confidence

Kết quả có thể không được sắp xếp theo thứ tự `confidence`. Trong trường hợp đó, kết quả trả về trước nên được tin tưởng hơn. `Confidence` dao động từ `0,0` đến` 1.0`.

`Confidence` có cách tính khác nhau cho từng loại:

**reverse geocoding** nó dựa trên khoảng cách từ điểm `reverse`. Cách tính `confidence` như sau:

| distance | confidence score |
| --- | --- |
| < 1 meter | 1.0 |
| 1 - 10 meters | 0.9 |
| 11 - 100 meters | 0.8 |
| 101 - 250 meters | 0.7 |
| 251 - 1000 meters | 0.6 |

**search and autocomplete** một số yếu tố ảnh hưởng đến điểm số `confidence`. Những yếu tố này là:

* the `match_type` được mô tả ở trên
* Đối với kết quả địa chỉ, thì`housenumber` and `street name` có đúng với input query
* Những trường thông tin khác có đúng với input query (trường `locality`,`county`,`region` ...).

Trong tất cả trường hợp, kết quả `confidence` = `fallback` sẽ bị hạn chế trong kết quả trả về.

### accuracy

`accuracy` cung cấp thông tin về độ chính xác của điểm vĩ độ và kinh độ được trả về với kết quả đã cho. Giá trị này là một thuộc tính của chính kết quả và sẽ không thay đổi dựa trên truy vấn. Hiện tại có hai giá trị `accuracy`: `point` và `centroid`.

`point` thường là địa chỉ, địa điểm hoặc địa chỉ nội suy. Kết quả điểm có nghĩa là có thể được biểu diễn một cách hợp lý bởi một điểm vĩ độ-kinh độ duy nhất.

`centroid` thường cho một khu vực lớn hơn, chẳng hạn như thành phố,quận/huyện hoặc tòa nhà. Hiện không thể trả về kết quả với hình học không gian (dạng vùng, dạng đường).
