# Vietmap Geocoder [v1.1]

## Nội Dung

### Các chức năng và tài liệu API

#### Mô tả thông tin API
    
```
    Tất cả API có format chung:
    
    https://maps.vietmap.vn/api/search?api-version=1.1&apikey={your-key}&text=vietmap
    \___/   \_____________/ \________/ \_____________/  \_____________/  \_________/
        |            |           |            |               |               |
    scheme       domain         path        version          key            query
```
- [Search](search.md) (**/api/search**)
    Cho phép tìm kiếm vị trí từ thông tin tên của cửa hàng, địa chỉ nhà.
    Đồng thời cũng cho phép 1 số các tùy chọn như tìm kiếm trong 1 vùng, tìm trong 1 bán kính cho trước.
- [Reverse](reverse.md) (**/api/reverse**)
    Lấy thông tin về địa điểm, đường, địa chỉ... từ một vị trí tọa độ nhất định.
- [Autocomplete](autocomplete.md) (**/api/autocomplete**)
    Đề xuất kết quả real-time và phù hợp nhất mà không cần phải nhập toàn bộ
- [Nearby](nearby.md) (**/api/nearby**) 
    Tìm kiếm thông tin xung quanh theo phân loại và theo bán kính


#### Tham số và các tùy chọn
- [Tham số của search,autocomplete](search.md#Available-search-parameters)
- [Tham số của reverse](reverse.md#Reverse-geocoding-parameters)
- [Tham số của nearby](nearby.md#Nearby-Parameters)

#### Mô tả thông tin trả về

- [Mô tả thông tin trả về](response.md)
- [Giải thích về confidence scores, match\_types](result_quality.md)

