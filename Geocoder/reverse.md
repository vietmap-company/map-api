# Reverse geocoding API

Reverse geocoding is  được sử dụng để tìm địa điểm hoặc địa chỉ gần cặp vĩ độ, kinh độ như nhấp vào bản đồ để xem thông tin tại vị trí điểm đó. Ví dụ: bản đồ hiển thị tòa nhà nhưng không có nhãn, sau đó nhấp vào tòa nhà thì hiển thị tên của doanh nghiệp.

Với reverse geocoding bạn có thể tra cứu tất cả các loại thông tin về các điểm trên bản đồ, bao gồm:

* address
* POI (doanh nghiệp, bảo tàng, công viên, vân vân)
* street (thông tin đường)

Bạn cần một cặp vĩ độ, kinh độ theo độ thập phân với các tham số `point.lat` và` point.lon` tương ứng. 
Ví dụ với tọa độ của công ty Vietmap: `10.758584896812293, 106.67527198791505` thì câu query:

>/api/reverse?__point.lat=10.758584896812293__&__point.lon=106.67527198791505__

[Kết quả trả về theo định dạng JSON](response.md).

## Reverse geocoding parameters

Giống như các API khác, Reverse có các parameters, tùy chọn mà bạn có thể sử dụng để tinh chỉnh kết quả.

Parameter | Type | Required | Default | Example
--- | --- | --- | --- | ---
`point.lat` | floating point number | yes | none | `10.758584896812293`
`point.lon` | floating point number | yes | none | `106.67527198791505`
`boundary.circle.radius` | floating point number | no | 1 | `0.5`
`size` | integer | no | `10` | `3`
`layers` | được phân cách bằng dấu phẩy | no | none (all layers) | `address,locality`
`api-version` | text | yes | 1.1 | 1.1 
### Size

Một tham số cơ bản để lọc là `size`, được sử dụng để giới hạn số lượng kết quả trả về. 

> /api/reverse?point.lat=10.758584896812293__&__point.lon=106.67527198791505&___size=1___

Giá trị mặc định `size` is `4` and the maximum value is `10`.

### Filter by layers (data type)

Khi bạn không chỉ định thêm, reverse geocoding không giới hạn kết quả với `layer` (đường phố, địa điểm, khu phố ...). Nếu ứng dụng của bạn quan tâm tới 1 layer cụ thể như: con đường nào gần nhất với vĩ độ, kinh độ được cho thì hãy sử parameter `layer`. 

> /api/reverse?point.lat=10.758584896812293&point.lon=106.67527198791505&___layers=street___

Dưới đây là tất cả các `layer` được hỗ trợ và ý nghĩa của chúng.

|layer|description|
|----|----|
|`venue`|tất cả mọi thứ trên đường: công ty, điểm nổi tiếng. .|
|`address`|dữ liệu địa chỉ|
|`street`|dữ liệu giao thông|
|`locality`|phường/xã|
|`county`|quận/huyện/thị xã/thị trấn|
|`region`|tỉnh/thành phố|


## Distance and confidence scores for the results

Mỗi kết quả được trả về có một khoảng cách `distance` từ điểm truy vấn (tính bằng mét) và điểm tin cậy `confidence`. Điểm tin cậy được tính dựa trên khoảng cách từ kết quả đến `point.lat` và` point.lon` được cung cấp. Điểm tin cậy của kết quả reverse có thể thay đổi với các nguồn dữ liệu và `layer` khác nhau.

Distance from `point.lat`/`point.lon` | Confidence score
--- | ---
&lt; 1m | 1.0
&lt; 10m | 0.9
&lt; 100m | 0.8
&lt; 250m | 0.7
&lt; 1km | 0.6
&gt;= 1km | 0.5
