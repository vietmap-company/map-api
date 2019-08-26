# Nearby API

## `Categories Filter`

### Functionality
- Là phần mở rộng của `/reverse` được dùng để tìm kiếm theo categories (nhà hàng, khách sạn, atm ..).
- Khác với `/search` và `/autocomplete` không yêu cầu parameter `text`.
- Chỉ có yêu cầu parameter `point`.
- Dùng parameter `categories` để thực hiện filter.
- Chấp nhận một giá trị hoặc danh sách giá trị được phân tách bằng dấu phẩy
- Khi nhiều giá trị được truyền vào `categories` thì tìm kiếm sẽ mang ý nghĩa OR giữa các giá trị

### Categorie Code
- Thông tin về từng loại code của `Categories` bạn có thể [tải về ở đây](/Geocoder/poicat/vietmap-poi-category.xlsx?raw=true)
- Bảng phân loại rất chi tiết giúp bạn tìm chính xác hơn.
### Validation

Dùng `categories` với 1 loại

`/api/nearby?categories=1000&point.lat=10.758584896812293&point.lon=106.67527198791505`

> Tìm kiếm ở vị trí focus những điểm ăn uống vì code 1000 là group ăn uống


Dùng `categories` với nhiều loại

`/api/nearby?categories=1001-1,1001-5&point.lat=10.758584896812293&point.lon=106.67527198791505`

> Tìm kiếm ở vị trí focus những điểm là Cafe hoặc Beer Club

### Nearby Parameters
Parameter | Type | Required | Default | Example
--- | --- | --- | --- | ---
`categories` | được phân cách bằng dấu phẩy | none | all | `1001-1,1001-5`
`point.lat` | floating point number | yes | none | `10.758584896812293`
`point.lon` | floating point number | yes | none | `106.67527198791505`
`boundary.circle.radius` | floating point number | no | 1 | `0.5`
`size` | integer | no | `10` | `3`
`layers` | được phân cách bằng dấu phẩy | no | none (all layers) | `address,locality`
`api-version` | text | yes | 1.1 | 1.1 
