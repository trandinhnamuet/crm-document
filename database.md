### Bảng: route_template

| Tên cột       | Kiểu dữ liệu  | Mô tả                                 |
|---------------|---------------|----------------------------------------|
| id            | SERIAL        | Khóa chính, tự tăng                   |
| code          | TEXT          | Mã lộ trình                            |
| name          | TEXT          | Tên lộ trình (tiếng Việt)             |
| start_date    | DATE          | Ngày bắt đầu lộ trình                 |
| end_date      | DATE          | Ngày kết thúc lộ trình                |
| repeat_type   | TEXT          | Kiểu lặp lại (`weekly`, `monthly`, ...) |
| repeat_on     | INTEGER       | Số tuần hoặc ngày lặp lại             |
| created_by    | INTEGER       | ID người tạo                          |
| created_at    | TIMESTAMP     | Thời gian tạo                         |
| updated_by    | INTEGER       | ID người cập nhật                     |
| updated_at    | TIMESTAMP     | Thời gian cập nhật                    |
| deleted_by    | INTEGER       | ID người xóa (nếu có)                 |
| deleted_at    | TIMESTAMP     | Thời gian xóa (nếu có)                |
| is_active     | BOOLEAN       | Trạng thái hoạt động (`true/false`)  |


### Bảng: customer

| Tên cột         | Kiểu dữ liệu        | Mô tả |
|------------------|----------------------|-------|
| `id`             | `SERIAL`             | Khóa chính, tự tăng |
| `code`           | `TEXT`               | Mã khách hàng |
| `name`           | `TEXT`               | Tên khách hàng (tiếng Việt) |
| `address`        | `TEXT`               | Địa chỉ (tiếng Việt) |
| `phone_number`   | `TEXT`               | Số điện thoại |
| `email`          | `TEXT`               | Email liên hệ |
| `note`           | `TEXT`               | Ghi chú thêm |
| `image_id`        | `INTEGER`            | ID ảnh đại diện (nếu có) |
| `latitude`       | `DOUBLE PRECISION`   | Vĩ độ (latitude) |
| `longitude`      | `DOUBLE PRECISION`   | Kinh độ (longitude) |
| `created_by`     | `INTEGER`            | ID người tạo |
| `created_at`     | `TIMESTAMP`          | Thời điểm tạo |
| `updated_by`     | `INTEGER`            | ID người cập nhật |
| `updated_at`     | `TIMESTAMP`          | Thời điểm cập nhật |
| `deleted_by`     | `INTEGER`            | ID người xóa (nếu có) |
| `deleted_at`     | `TIMESTAMP`          | Thời điểm xóa (soft delete) |
| `is_active`      | `BOOLEAN`            | Trạng thái hoạt động |

### Bảng: route_template_customer 

| Tên cột             | Kiểu dữ liệu | Ràng buộc                                | Mô tả |
|---------------------|--------------|-------------------------------------------|-------|
| `id`                | SERIAL       | PRIMARY KEY                              | ID tự tăng, định danh duy nhất |
| `route_template_id` | INTEGER      | NOT NULL                                 | ID của mẫu lộ trình (`route_template`) |
| `customer_id`       | INTEGER      | NOT NULL                                 | ID của khách hàng sẽ được ghé thăm |


### Bảng: route_instance

| Tên cột             | Kiểu dữ liệu   | Ràng buộc                                      | Mô tả |
|---------------------|----------------|------------------------------------------------|-------|
| `id`                | SERIAL         | PRIMARY KEY                                    | ID tự tăng, định danh duy nhất cho mỗi lần đi tuyến |
| `route_template_id` | INTEGER        | NOT NULL, FOREIGN KEY → `route_template(id)` ON DELETE CASCADE | Khóa ngoại liên kết với mẫu tuyến ban đầu |
| `start_date`        | DATE           | NOT NULL                                       | Ngày bắt đầu chuyến đi |
| `end_date`          | DATE           | NULLABLE                                       | Ngày kết thúc chuyến đi (nếu có) |
| `is_finished`       | BOOLEAN        | DEFAULT FALSE                                  | Cờ đánh dấu chuyến đi đã hoàn thành hay chưa |
| `created_at`        | TIMESTAMP      | DEFAULT CURRENT_TIMESTAMP                      | Thời điểm tạo bản ghi |


### Bảng: route_instance_customer 

| Tên cột             | Kiểu dữ liệu   | Ràng buộc                                                | Mô tả |
|---------------------|----------------|------------------------------------------------------------|-------|
| `id`                | SERIAL         | PRIMARY KEY                                                | ID tự tăng, định danh duy nhất |
| `route_instance_id` | INTEGER        | NOT NULL, FOREIGN KEY → `route_instance(id)` ON DELETE CASCADE | Liên kết đến chuyến đi cụ thể |
| `customer_id`       | INTEGER        | NOT NULL, FOREIGN KEY → `customer(id)` ON DELETE CASCADE       | Khách hàng thuộc chuyến đi này |
| `is_visited`        | BOOLEAN        | DEFAULT FALSE                                              | Đã ghé thăm khách hàng hay chưa |
| `checkin_at`        | TIMESTAMP      | NULLABLE                                                   | Thời gian bắt đầu gặp khách |
| `checkout_at`       | TIMESTAMP      | NULLABLE                                                   | Thời gian kết thúc buổi gặp |
| `note`              | TEXT           | NULLABLE                                                   | Ghi chú thêm cho lần ghé thăm |

### Bảng: image

| Tên cột        | Kiểu dữ liệu       | Mô tả |
|----------------|--------------------|-------|
| `id`           | `SERIAL`           | Khóa chính, tự tăng |
| `file_name`    | `TEXT`             | Tên file ảnh gốc (vd: avatar.jpg) |
| `link`         | `TEXT`             | Đường dẫn truy cập ảnh (nếu lưu file bên ngoài hoặc cloud) |
| `mime_type`    | `TEXT`             | Loại file (vd: image/png, image/jpeg) |
| `image_data`   | `BYTEA`            | Dữ liệu nhị phân của ảnh (chỉ dùng nếu lưu ảnh trực tiếp trong DB) |
| `created_at`   | `TIMESTAMP`        | Thời điểm tạo ảnh (mặc định là `CURRENT_TIMESTAMP`) |


### Bảng: route_instance_customer_image 

| Tên cột                    | Kiểu dữ liệu  | Mô tả |
|----------------------------|---------------|-------|
| `id`                       | `SERIAL`      | Khóa chính, tự tăng |
| `route_instance_customer_id` | `INTEGER`   | Khóa ngoại đến bảng `route_instance_customer(id)` |
| `image_id`                 | `INTEGER`     | Khóa ngoại đến bảng `image(id)` |

### Bảng: user

| Tên cột        | Kiểu dữ liệu | Ràng buộc              | Mô tả |
|----------------|--------------|-------------------------|-------|
| `id`           | SERIAL       | PRIMARY KEY             | ID tự tăng, định danh người dùng |
| `username`     | TEXT         | NOT NULL, UNIQUE        | Tên đăng nhập, duy nhất trong hệ thống |
| `password`     | TEXT         | NOT NULL                | Mật khẩu của người dùng (nên mã hóa khi lưu) |
| `fullname`     | TEXT         |                         | Họ và tên đầy đủ của người dùng |
| `phone_number` | TEXT         |                         | Số điện thoại liên lạc |
| `date_of_birth`| DATE         |                         | Ngày sinh của người dùng |
| `email`        | TEXT         | UNIQUE                  | Địa chỉ email, duy nhất |
| `image_id`     | INTEGER      |                         | ID ảnh đại diện (tham chiếu bảng `image`) |
| `created_at`   | TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP | Thời điểm tạo tài khoản |