# Search results

Bạn sẽ luôn nhận được kết quả JSON, trừ khi có lỗi nghiêm trọng, trong trường hợp đó bạn sẽ nhận được thông báo lỗi.

Cấu trúc của mỗi kết quả trả về:

```
{
    "code": [...],
    "message": [...],
    "data":{
        "type":"FeatureCollection",
        "features":[...],
        "bbox":[...]
    }
}
```
`code` có 2 loại : `OK` , `ERROR`

`message`: sẽ có giá trị khi `code`=`ERROR`, thể hiện thông tin lỗi

`data`: có giá trị khi `code`=`OK`

## List of features returned

Thuộc tính `features` của kết quả là nơi bạn sẽ tìm thấy danh sách kết quả phù hợp nhất với các tham số đầu vào của bạn.

Mỗi đối tượng này sẽ chứa tất cả thông tin cần thiết `properties` và tọa độ `geometry`.

```
{
    "code": "OK",
    "message": null,
    "data": {
        "features": [
            {
                "type": "Feature",
                "geometry": {
                    "type": "Point",
                    "coordinates": [
                        106.689785,
                        10.770366
                    ]
                },
                "properties": {
                    "layer": "street",
                    "name": "HẺM 150 Nguyễn Trãi",
                    "street": "HẺM 150 Nguyễn Trãi",
                    "confidence": 0.9,
                    "distance": 0.002,
                    "accuracy": "centroid",
                    "country": "Vietnam",
                    "region": "Thành phố Hồ Chí Minh",
                    "county": "Quận 1",
                    "locality": "Phường Bến Thành",
                    "label": "HẺM 150 Nguyễn Trãi, Phường Bến Thành, Vietnam"
                },
                "bbox": [
                    106.689574,
                    10.770084,
                    106.689999,
                    10.770649
                ]
            }
        ],
        "type": "FeatureCollection",
        "bbox": [
            106.689574,
            10.770084,
            106.689999,
            10.770649
        ],
        "license": "vietmap"
    }
}
```

Đối với, [/api/reverse](reverse.md) sẽ có thêm `distance` parameter, đơn vị tính là meter tính từ point query.

## Notable features

## `coordinates`

Tất cả các kết quả được trả về là các điểm và có thể được tìm thấy trong  `coordinates`. Xem thêm [GeoJSON specification](http://geojson.org/geojson-spec.html#positions), để biết thứ tự của **longitude, latitude**.

### `name`

`name` là một mô tả ngắn về địa điểm, chẳng hạn như tên doanh nghiệp, tên địa phương hoặc một phần của địa chỉ, tùy thuộc vào những gì đang được tìm kiếm.

Đối với tìm kiếm địa chỉ, các thuộc tính `housenumber` và` street` được kết hợp với nhau vào thuộc tính` name` . Điều này giúp bạn không phải tự sắp xếp lại địa chỉ, bao gồm để xác định xem các số nên được đặt trước hay sau tên đường.

### `label`

`label` thể hiện khá thân thiện với con người về địa điểm, với các thông tin cần thiết, đã sẵn sàng để được hiển thị cho người dùng cuối. Ví dụ `label` bao gồm tên doanh nghiệp hoặc địa điểm với địa phương, địa chỉ gửi thư đầy đủ hoặc địa phương có tên khu vực.

### `confidence`

`confidence` là ước tính mức độ chính xác của kết quả này phù hợp với truy vấn.

Đối với [/api/reverse](reverse.md), điểm tin cậy chỉ được xác định bởi khoảng cách từ tọa độ được chỉ định. Kết quả gần hơn sẽ được điểm cao hơn.

Đối với [/api/search](search.md) chủ yếu sẽ tính đến việc các thuộc tính trong kết quả khớp với những gì được mong đợi từ việc phân tích văn bản đầu vào. Ví dụ: nếu văn bản đầu vào trông giống như một địa chỉ, nhưng số nhà của kết quả không khớp với số nhà được phân tích cú pháp từ văn bản đầu vào, điểm tin cậy sẽ thấp hơn.

### `bbox`

`bbox` nó mô tả phạm vi địa lý của đối tượng, chẳng hạn như kích thước màn hình cần thiết để hiển thị tất cả mà không cần gửi hình dạng đa giác chính xác.
