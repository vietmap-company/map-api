# Search API

Trong tìm kiếm đơn giản nhất, bạn chỉ cần cung cấp một tham số nội dung, bạn sẽ nhận được thông tin khớp với nội dung bạn truyền vào. Để làm điều này, xây dựng một query trong đó `text` parameter với nội dung bạn muốn tìm.

Ví dụ, bạn muốn tìm địa chỉ: 193 Trần Phú

> [/api/search?api-version=1.1&apiley={your-key}&__text=193 Trần Phú__](https://maps.vietmap.vn/api/search?text=193%20tr%E1%BA%A7n%20ph%C3%BA)

Bảng thông tin giá trị parameter như sau:

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |

Dữ liệu trả về [JSON](/response.md).


Lưu ý rằng kết quả được trải rộng trên toàn lãnh thổ Việt Nam vì bạn chưa đưa ra vị trí hiện tại của mình hoặc cung cấp bất kỳ thông tin địa lý nào khác để tìm kiếm.

## Size

Theo mặc định, kết quả lên tới 10 vị trí, trừ khi có quy định khác. Nếu bạn muốn có số lượng kết quả khác nhau, hãy đặt tham số `size` thành số bạn muốn. Ví dụ này cho thấy chỉ trả về kết quả đầu tiên.

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `size` | 1 |

> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__size=1__](https://maps.vietmap.vn/api/search?text=193%20tr%E1%BA%A7n%20ph%C3%BA&size=1&apikey=)

Nếu bạn muốn có 15 kết quả, bạn hãy chỉnh `size` thành 15.

> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__size=15__](https://maps.vietmap.vn/api/search?text=193%20tr%E1%BA%A7n%20ph%C3%BA&size=15&apikey=)

## Narrow your search (Thu hẹp tìm kiếm)

Nếu bạn đang tìm kiếm các địa điểm trong một khu vực hoặc chỉ muốn tìm trong vùng lân cận ngay lập tức của người dùng với một vị trí đã biết, bạn có thể thu hẹp tìm kiếm của mình vào một khu vực. Có nhiều cách khác nhau để bao gồm một vùng trong truy vấn của bạn. Hiện tại hỗ trợ các loại sau: hình chữ nhật và hình tròn.

### Search within a rectangular region (Tìm kiếm theo khu vực)

Để chỉ định ranh giới bằng hình chữ nhật, bạn cần tọa độ vĩ độ, kinh độ cho hai đường chéo giới hạn.

Ví dụ, để tìm 193 Trần Phú trong thành phố Hồ Chí Minh, bạn cần bổ sung  `boundary.rect.*` `min_lon`=106.3564 `min_lat`=10.376715 `max_lon`=107.012794 `max_lat`=11.160291


> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__boundary.rect.min_lat=10.376715&boundary.rect.min_lon=106.3564&boundary.rect.max_lat=11.160291&boundary.rect.max_lon=107.012794__](https://maps.vietmap.vn/api/search?boundary.rect.min_lat=10.376715&boundary.rect.min_lon=106.3564&boundary.rect.max_lat=11.160291&boundary.rect.max_lon=107.012794&text=193%20Tr%E1%BA%A7n%20Ph%C3%BA&api-version=1.1)

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `boundary.rect.min_lat` | 10.376715 |
| `boundary.rect.min_lon` | 106.3564 |
| `boundary.rect.max_lat` | 11.160291 |
| `boundary.rect.max_lon` | 107.012794 |


### Search within a circular region (Tìm kiếm theo bán kính)

Đôi khi bạn có vị trí của điểm và một bán kính ta có thể tìm kiếm theo bán kính.

Trong ví dụ này, nếu bạn muốn tìm những điểm 193 Trần Phú trong bán kính 0.5 km. Bạn hãy dùng nhóm parameter `boundary.circle.*` với `boundary.circle.lat` và `boundary.circle.lon` là vị trí của bạn, `boundary.circle.radius` là bán kính tìm tính từ khoảng vị trí của điểm. Lưu ý `boundary.circle.radius` luôn được tính theo kilometer.

> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__boundary.circle.lon=106.661280&boundary.circle.lat=10.756271&boundary.circle.radius=0.5__](https://maps.vietmap.vn/api/search%3Fboundary.circle.lon=10.756271&boundary.circle.lat=10.756271&boundary.circle.radius=0.5&text=193%20tr%E1%BA%A7n%20ph%C3%BA&api-version=1.1)

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `boundary.circle.lat` | 10.756271 |
| `boundary.circle.lon` | 106.661280 |
| `boundary.circle.radius` | 0.5 |

### Prioritize around a point (Tìm kiếm ưu tiên)

Bằng cách chỉ định một `focus.point`, kết quả sẽ được sắp xếp một phần theo mức độ gần với tọa độ đã cho. Tất cả những thứ khác đều giống nhau, kết quả gần với điểm sẽ được ưu tiên. Tuy nhiên, không giống tham số
 `boundary.circle`, với điểm xa tọa độ đã cho vẫn có thể được trả về. Ví dụ, [tìm những điểm của thế giới di động với `focus.point` là vị trí ở Quận 5, Tp Hồ Chí Minh](https://maps.vietmap.vn/api/autocomplete?focus.point.lat=10.756271&focus.point.lon=106.661280&text=the%20gioi%20di%20dong&api-version=1.1).


> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__focus.point.lat=-33.856680&focus.point.lon=151.215281__](https://maps.vietmap.vn/api/search?focus.point.lat=10.756271&focus.point.lon=106.661280&text=the%20gioi%20di%20dong&api-version=1.1)

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `focus.point.lat` | 10.756271 |
| `focus.point.lon` | 106.661280 |

Nhìn vào kết quả, bạn có thể thấy rằng một vài vị trí gần vị trí này hiển thị ở đầu danh sách, được sắp xếp theo khoảng cách.

## Combine boundary search and prioritizatio (Kết hợp tìm kiếm ưu tiên và tìm theo khu vực)

Như bạn đã thấy bằng cách sử tìm kiếm theo khu vực và tìm kiếm ưu tiên để thu hẹp và sắp xếp kết quả của mình, bạn có thể thử dùng cả 2 vì chúng hoạt động tốt với nhau.

## Filter your search

Dữ liệu Vietmap được phân thành nhiều layers và kết hợp nhiều loại địa điểm vào một cơ sở dữ liệu, cho phép bạn tùy chọn để chọn tập dữ liệu bạn muốn tìm kiếm.

Hiện tại hỗ trợ truy vấn dữ liệu theo layer:

* `layer`: loại layer bạn muốn tìm


## Filter by layers (data type)

Dưới đây là danh sách các `layer` bạn có thể tìm thấy trong kết quả, sắp xếp theo độ chi tiết:

|layer|description|
|----|----|
|`venue`|tất cả mọi thứ trên đường: công ty, điểm nổi tiếng. .|
|`address`|dữ liệu địa chỉ|
|`street`|dữ liệu giao thông|
|`locality`|phường/xã|
|`county`|quận/huyện/thị xã/thị trấn|
|`region`|tỉnh/thành phố|

> [/api/search?api-version=1.1&apiley={your-key}&text=193 Trần Phú&__layers=venue,address__](https://maps.vietmap.vn/api/search?text=the%20gioi%20di%20dong&api-version=1.1&layers=venue,address)

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `layers` | venue,address |

## Available search parameters

| Parameter | Type | Required | Default | Example |
| --- | --- | --- | --- | --- |
| `text` | string | yes | none | `Trần Phú` |
| `focus.point.lat` | floating point number | no | none | `10.756271` |
| `focus.point.lon` | floating point number | no | none | `106.661280` |
| `boundary.rect.min_lon` | floating point number | no | none | `106.3564` |
| `boundary.rect.max_lon` | floating point number | no | none | `107.012794` |
| `boundary.rect.min_lat` | floating point number | no | none | `11.160291` |
| `boundary.rect.max_lat` | floating point number | no | none | `10.376715` |
| `boundary.circle.lat` | floating point number | no | none | `10.756271` |
| `boundary.circle.lon` | floating point number | no | none | `106.661280` |
| `boundary.circle.radius` | floating point number | no | 50 | `35` |
| `layers` | string | no | all layers: address,venue,locality,county,region,country | address,venue |
| `size` | integer | no | 10 | 20 |