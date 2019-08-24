# Search with autocomplete API

Nếu bạn đang xây dựng một ứng dụng người dùng cuối, bạn có thể sử dụng `/autocomplete` cùng với `/search` để kích hoạt real-time feedback. Chức năng này giúp người dùng tìm thấy những gì họ đang tìm kiếm mà không yêu cầu họ chỉ định đầy đủ nội dung tìm kiếm của họ. Thông thường, người dùng bắt đầu nhập và một danh sách thả xuống xuất hiện nơi họ có thể chọn từ danh sách bên dưới.

Để xây dựng một truy vấn với `autocomplete` bạn cần một tham số `text`, đại diện cho những gì người dùng đã nhập vào ứng dụng của bạn. Bạn có thể chỉ định một điểm nơi tìm kiếm sẽ tập trung, điều này sẽ cho phép người dùng xem nhiều kết quả hơn.

## Set the number of results returned

Theo mặc định kết quả trả về lên tới 10 vị trí, trừ khi có quy định khác. Nếu bạn muốn có số lượng kết quả khác nhau, hãy đặt parameter `size` thành số mong muốn. Ví dụ này chỉ trả về kết quả đầu tiên.

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần |
| `size` | 1 |

> [/api/autocomplete?api-version=1.1&apiley={your-key}&text=193 Trần&__size=1__](https://maps.vietmap.vn/api/autocomplete?text=193%20tran&api-version=1.1&size=1)

Nếu bạn muốn có 15 kết quả thì `size` bạn sẽ là 15.

> [/api/autocomplete?api-version=1.1&apiley={your-key}&text=193 Trần&__size=15__](https://maps.vietmap.vn/api/autocomplete?text=193%20tran&api-version=1.1&size=15)

## Global scope, local focus

Để tập trung tìm kiếm của bạn dựa trên một khu vực địa lý, chẳng hạn như trung tâm  bản đồ của người dùng hoặc tại vị trí GPS của thiết bị, hãy cung cấp các tham số `focus.point.lat` và `focus.point.lon`. Điều này làm tăng kết quả liên quan cao hơn.

> /api/autocomplete?api-version=1.1&apiley={your-key}&__focus.point.lat=10.756271&focus.point.lon=106.661280__&text=Ngân Hàng

## Filters

### Layers

Dưới đây là danh sách các `layer` bạn có thể tìm thấy trong kết quả, sắp xếp theo độ chi tiết:

|layer|description|
|----|----|
|`venue`|tất cả mọi thứ trên đường: công ty, điểm nổi tiếng. .|
|`address`|dữ liệu địa chỉ|
|`street`|dữ liệu giao thông|
|`locality`|phường/xã|
|`county`|quận/huyện/thị xã/thị trấn|
|`region`|tỉnh/thành phố|

> /api/autocomplete?api-version=1.1&apiley={your-key}&__layers=venue__&text=ngan hang

`layers=venue` bạn sẽ chỉ nhìn thấy các địa điểm có tên là ngân hàng

### Search within a circular region

Đôi khi bạn có vị trí của điểm và một bán kính ta có thể tìm kiếm theo bán kính.

Trong ví dụ này, nếu bạn muốn tìm những điểm 193 Trần Phú trong bán kính 0.5 km. Bạn hãy dùng nhóm parameter `boundary.circle.*` với `boundary.circle.lat` và `boundary.circle.lon` là vị trí của bạn, `boundary.circle.radius` là bán kính tìm tính từ khoảng vị trí của điểm. Lưu ý `boundary.circle.radius` luôn được tính theo kilometer.

> [/api/autocomplete?text=Vietmap&__boundary.circle.lon=106.661280&boundary.circle.lat=10.756271&boundary.circle.radius=0.5__](https://maps.vietmap.vn/api/autocomplete%3Fboundary.circle.lon=106.661280&boundary.circle.lat=10.756271&boundary.circle.radius=0.5&text=Vietmap)

| parameter | value |
| :--- | :--- |
| `text` | 193 Trần Phú |
| `boundary.circle.lat` | 10.756271 |
| `boundary.circle.lon` | 106.661280 |
| `boundary.circle.radius` | 0.5 |

## Available autocomplete parameters

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
| `api-version` | text | yes | 1.1 | 1.1 |
