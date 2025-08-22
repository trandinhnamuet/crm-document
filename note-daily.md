#07/07/2025
##Đăng ký google cloud console, tạo API google map đăng ký bằng trandinhnam9095@gmail.com
https://console.cloud.google.com/apis/credentials?project=dev-ruler-466004-c9
AIzaSyD8PJk4BXaTbPjsYamAN70o1r98AnNAQWs

#09/07/2025

##8h: Xem demo đi tuyến, thiết kế database cho đi tuyến.

##9h: Khởi tạo FE:React, Vite. Khởi tạo BE:NestJS. Tải và cài Postgresql. Push code lên github repo.

(https://github.com/trandinhnamuet/crm-document)

(https://github.com/trandinhnamuet/crm-frontend)

(https://github.com/trandinhnamuet/crm-backend)

##10h: Tạo 7 bảng customer, route_template, route_instance, route_template_customer, route_instance_customer, image, route_template_customer_image

##10h50: Cấu hình backend với database. Tạo CRUD cho 4 bảng customer route_template route_instance user

##11h30: Tạo trang CRUD cho 4 bảng trên. Cài Tailwind bị lỗi do tailwind 4 bị điên. Cuối cùng fix bằng xóa đi cài lại tailwind 3. 12h46 mới fix xong. -> Cụ thể hoàn thiện được như video https://www.youtube.com/watch?v=-7k2QUZdW0g

#09/08/2025
##Kiểm tra nếu chưa đăng nhập thì dù vào màn nào cũng tự dẫn về màn /login

#11/08/2025
##Bổ sung route_instance_customer module cho backend (đáng ra thêm từ trước nhưng bị sót)
##Triển khai lên server online free
###Frontend: Vercel                      link
###Backend: Render                       https://dashboard.render.com/web/srv-d1qvrugdl3ps73esm1o0
###Database: Supabase                    https://supabase.com/dashboard/project/dfhkhcashblphprgrapx

#20/08/2025
##Thêm cronjob hàng ngày kiểm tra hôm nay có route template nào đến ngày lặp lại không, nếu có thì tạo route_instance và route_instance_customer tương ứng

##Thu nhỏ map để chứa toàn bộ điểm định vị khách hàng trong tuyến
##Bổ sung thêm vài cột trong màn Route Instance
##Thêm cắm mốc vị trí hiện tại


#21/08/2025

##Thêm folder services và viết file service call api cho frontend với từng controller backend. Sau này frontend call api đều sẽ qua các service này thay vì call trực tiếp tại component: auth,user,customer ,route_instance,route_instance_customer,route_template,route_template_customer

##Hiện tại màn RouteInstanceDetail đang show list cusotmer/by route template thay vì route instance customer => sửa

##Bật APi tính khoảng cách xe máy: check thấy Directions API, Distance Matrix API đều đã bật -> call ko được do call trực tiếp từ frontend
-> Thêm module call google api cho backend

##Fix lỗi frontend các route đều hoạt động đúng nhưng riêng route /route-instance-detail/id thì bị 404 Not found như https://crm-frontend-git-main-tran-dinh-nams-projects.vercel.app/route-instance-detail/13.
-> tạo file vercel.json

##Thêm trường người phụ trách tuyến cho bảng route template và route instance. Người phụ trách của route template có thể thay đổi. Route instance khi được tạo từ template sẽ gắn với người phụ trách hiện tại của template

##Thêm chức năng tạo route instance và route instance customer ngay lập tức cho 1 template (chạy khi user kích hoạt hoặc khi mới tạo template) -> UI màn tạo template cần thêm 1 checkbox có tạo instance ngay không

##Thêm folder migrations để chính sửa database bằng code mỗi khi chạy mới backend

##Sửa logic tính start date và end date cho route instance khi tạo mới: Cover trường hợp repeat on = 7 nhưng hàm chạy vào thứ 5 (do user kích hoạt) -> end date thành thứ 4 tuần sau (vì logic end date = start date + 7), đến thứ 7 cronjob lại chạy tạo route instance mới cho template với start end date là thứ 6 tuần sau -> có khoảng thời gian mà 2 route instance trùng template cùng tồn tại 
-> sau update: 
- weekly repeat_on=5: start date = thứ 5, end date = thứ 4 tuần sau
- monthly repeat_on=5:




22/08

- Data checkin nhưng chưa checkout lưu vào đâu? Checkin_at và checkout_at, nếu null thì là false
- Thêm module backend route instance customer image + image, thêm api upload ảnh cho route instance customer

- Sắp xếp các khách hàng trong 1 route instance: theo is_visited, sau đó theo khoảng cách chim bay

- Làm màn Đi tuyến 1 khách hàng RouteInstanceCustomerDetail: show thông tin, show list ảnh, button thêm ảnh, checkin checkout

- Thêm màn lịch sử thăm 1 customer

- Update UI hàng loạt để show giao diện đẹp trên điện thoại
- Thêm màn thông tin cá nhân để xem và sửa thông tin tài khoản 
- Dark/light mode cho side bar menu. Thêm icon cho các option
- Thêm button chỉ đường trong phiên làm việc
- Thêm đủ 4 phương thức nhập địa chỉ của khách hàng
- Thêm đủ 4 phương thức nhập địa chỉ của khách hàng
- Thêm Chức năng: xem lịch sử đi tuyến 1 customer 

Todo:
- Fix: Đang check in được dù chưa checkout
- Fix: Đã đi hết route instance customer nhưng route instance vẫn ghi trạng thái chưa hoàn thành
- thêm cột route instance: đây là lần đi thứ bao nhiêu của tuyến này    
- thêm trường role cho bảng user để làm phân quyền
- Trang chủ: Show thông tin tổng quan như list tuyến và % hoàn thành từng tuyến. Cột update tình hình đi tuyến mới nhất: Note + Ảnh. Số tuyến đang hoạt động: 7. Số khách hàng đang trong tuyến: 112. 
- Bấm vào label sẽ mở link google map dẫn đường. Thêm button chỉ đường cho Card
- Show thêm số lần đã hoàn thành của 1 tuyến

- Thêm màn thông tin chi tiết lộ trình để xử lý vấn đề màn list lộ trình, cột actions đang có quá nhiều button
##Phân quyền ai nhìn thấy gì

##Thêm 1 bảng setting lưu các setting như bao lâu thì đăng xuất


##Route Instance là màn chỉ nhìn, không nên có edit hay thêm mới


- Chức năng lập lộ trình thông minh để khoảng cách di chuyển là tối thiểu

- Nếu có nhu cầu đi thăm khách hàng không có trong lộ trình đi tuyến hôm nay thì sao?

- Confirm lại xem mật khẩu sẽ cho admin toàn quyền xem sửa hay ai chỉ biết mật khẩu của người đó, admin cũng không xem được?



- Thêm list khách hàng chưa có định vị ra, thêm chức năng lưu/ cập nhật địa chỉ khách hàng trong phiên làm việc đi tuyến với khách hàng đó





