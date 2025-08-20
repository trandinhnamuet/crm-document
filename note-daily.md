# 09/07/2025

## 8h: Xem demo đi tuyến, thiết kế database cho đi tuyến.

## 9h: Khởi tạo FE:React, Vite. Khởi tạo BE:NestJS. Tải và cài Postgresql. Push code lên github repo.

(https://github.com/trandinhnamuet/crm-document)

(https://github.com/trandinhnamuet/crm-frontend)

(https://github.com/trandinhnamuet/crm-backend)

## 10h: Tạo 7 bảng customer, route_template, route_instance, route_template_customer, route_instance_customer, image, route_template_customer_image

## 10h50: Cấu hình backend với database. Tạo CRUD cho 4 bảng customer route_template route_instance user

## 11h30: Tạo trang CRUD cho 4 bảng trên. Cài Tailwind bị lỗi do tailwind 4 bị điên. Cuối cùng fix bằng xóa đi cài lại tailwind 3. 12h46 mới fix xong. -> Cụ thể hoàn thiện được như video https://www.youtube.com/watch?v=-7k2QUZdW0g

# 09/08/2025
## Kiểm tra nếu chưa đăng nhập thì dù vào màn nào cũng tự dẫn về màn /login

# 11/08/2025
## Bổ sung route_instance_customer module cho backend (đáng ra thêm từ trước nhưng bị sót)

# 20/08/2025
## Thêm cronjob hàng ngày kiểm tra hôm nay có route template nào đến ngày lặp lại không, nếu có thì tạo route_instance và route_instance_customer tương ứng

Todo:

## Hoàn thiện chức năng màn đi tuyến:
### Show thông tin thẻ
### Checkin, Checkout
### Đánh dấu customer đã đi
### 

## THêm chức năng tạo route instance và route instance customer ngay lập tức cho 1 template (chạy khi user kích hoạt hoặc khi mới tạo template) -> UI màn tạo template cần thêm 1 checkbox có tạo instance ngay không

## Chỉnh sửa UI cho desktop
## Update UI cho mobile

## Add 3 phương thức ghi định vị cho khách hàng: Get vị trí hiện tại, cắm trên bản đồ, nhập link google map
## Thêm 1 bảng setting lưu các setting như bao lâu thì đăng xuất
## Phân quyền ai nhìn thấy gì
