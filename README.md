# BÁO CÁO THỰC HÀNH KIỂM THỬ API BẰNG POSTMAN

## 1. Thông tin bài thực hành

- **Họ và tên:** Đồng Thị Ánh
- **Công cụ sử dụng:** Postman
- **API sử dụng:** JSONPlaceholder
- **Repository:** Postman-api-testing

---

## 2. Mục tiêu

Bài thực hành nhằm tìm hiểu và sử dụng công cụ Postman để kiểm thử API.

Các nội dung thực hiện gồm:

- Gửi HTTP Request bằng Postman.
- Kiểm tra HTTP Status Code.
- Kiểm tra dữ liệu trả về từ API.
- Sử dụng Postman Test Scripts để tự động kiểm tra kết quả.
- Thực hiện kiểm thử với các phương thức HTTP:
  - GET
  - POST
  - PUT
  - DELETE
- Kiểm thử cả trường hợp API hoạt động thành công và trường hợp API trả về lỗi.

---

## 3. Công cụ và môi trường

### Công cụ

- Postman
- GitHub
- JSONPlaceholder REST API

### API Base URL
https://jsonplaceholder.typicode.com
# 4. Chi tiết thực hiện

## 4.1. Test Case 01 - GET All Users

### Mục đích
Kiểm tra API có trả về danh sách Users hay không.
### Request
GET https://jsonplaceholder.typicode.com/users
### Kết quả mong đợi
- HTTP Status Code: 200 OK
- Response trả về một mảng dữ liệu Users.
- Mảng Users có ít nhất một phần tử.
### Test Script:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


pm.test("Response contains users", function () {
    const data = pm.response.json();
    pm.expect(data).to.be.an("array");
    pm.expect(data.length).to.be.greaterThan(0);
});
### Hình ảnh minh họa
<img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/42cb0c5a-f932-41f0-8f3f-3f5f461c6d6c" />

## 4.2 Test Case 02 - GET User By ID
### Mục đích
Kiểm tra khả năng lấy thông tin một User cụ thể thông qua ID.
### Request
GET https://jsonplaceholder.typicode.com/users/1
### Kết quả mong đợi
- HTTP Status Code: 200 OK
- User trả về có id = 1.
### Test Script
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("User ID is 1", function () {
    const data = pm.response.json();
    pm.expect(data.id).to.eql(1);
});
## Hình ảnh minh họa
<img width="1920" height="1029" alt="image" src="https://github.com/user-attachments/assets/cc76185c-1c52-4630-83c5-f2d53fa77580" />

## 4.3. Test Case 03 - GET Invalid User
### Mục đích
Kiểm tra API khi yêu cầu một User không tồn tại.
### Request
GET https://jsonplaceholder.typicode.com/users/9999
### Kết quả mong đợi
HTTP Status Code: 404 Not Found
Response body là {}.
### Test Script
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Response body is empty", function () {
    const data = pm.response.json();
    pm.expect(data).to.eql({});
});
### Hình ảnh minh họa 
<img width="1920" height="1028" alt="image" src="https://github.com/user-attachments/assets/968e6aa7-7c53-4b1e-937a-f675af5ec6f0" />

## 4.4. Test Case 04 - POST Create User
### Mục đích
Kiểm tra khả năng tạo một User mới bằng phương thức POST.
### Request
POST https://jsonplaceholder.typicode.com/users
### Request Body
{
    "name": "Anh Dong",
    "username": "anhdong",
    "email": "anhdong@example.com"
}
### Kết quả mong đợi
- HTTP Status Code: 201 Created
- Response trả về thông tin User vừa gửi.
- Dữ liệu Response khớp với dữ liệu trong Request Body.
### Test Script
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Created user has correct data", function () {
    const data = pm.response.json();

    pm.expect(data.name).to.eql("Anh Dong");
    pm.expect(data.username).to.eql("anhdong");
    pm.expect(data.email).to.eql("anhdong@example.com");
});
### Hình ảnh minh họa 
<img width="1920" height="1025" alt="image" src="https://github.com/user-attachments/assets/998cfd99-3f71-489e-b777-94c0f97dcd95" />

## 4.5. Test Case 05 - PUT Update User
### Mục đích
Kiểm tra khả năng cập nhật thông tin User bằng phương thức PUT.
### Request
PUT https://jsonplaceholder.typicode.com/users/1
### Request Body
{
    "name": "Anh Dong Updated",
    "username": "anhdong_updated",
    "email": "anhdong_updated@example.com"
}
### Kết quả mong đợi
- HTTP Status Code: 200 OK
- User có ID bằng 1.
- Thông tin User được cập nhật đúng.
### Test Script
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("User was updated correctly", function () {
    const data = pm.response.json();

    pm.expect(data.id).to.eql(1);
    pm.expect(data.name).to.eql("Anh Dong Updated");
    pm.expect(data.username).to.eql("anhdong_updated");
    pm.expect(data.email).to.eql("anhdong_updated@example.com");
});
### Hình ảnh minh họa 
<img width="1917" height="1032" alt="image" src="https://github.com/user-attachments/assets/1c485f80-3321-4128-83ed-59127f7461c9" />

## 4.6. Test Case 06 - DELETE User
### Mục đích
Kiểm tra khả năng thực hiện thao tác DELETE User.
### Request
DELETE https://jsonplaceholder.typicode.com/users/1
### Kết quả mong đợi
- HTTP Status Code: 200 OK
- Response body là {}.
### Test Script
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response body is empty", function () {
    const data = pm.response.json();
    pm.expect(data).to.eql({});
});
### Hình ảnh minh họa
<img width="1915" height="1032" alt="image" src="https://github.com/user-attachments/assets/4dc90583-8919-466b-b00f-1ef1abe06537" />

## 5. Đánh giá kết quả
Qua quá trình thực hành, các API Request đều trả về kết quả phù hợp với kết quả mong đợi.
Các Test Case đã thực hiện:
- GET danh sách Users.
- GET User theo ID.
- Kiểm tra User không tồn tại.
- POST tạo User.
- PUT cập nhật User.
- DELETE User.
Bài thực hành đã kiểm tra cả:
- HTTP Status Code.
- Response Body.
- Kiểu dữ liệu Response.
- Giá trị các trường dữ liệu.
- Trường hợp API trả về lỗi.
## 6. Kết luận
Qua bài thực hành, em đã làm quen với công cụ Postman và quy trình kiểm thử REST API.
Em đã thực hiện được:
- Tạo Collection trong Postman.
- Tạo và gửi HTTP Request.
- Sử dụng các phương thức GET, POST, PUT và DELETE.
- Kiểm tra HTTP Status Code.
- Kiểm tra dữ liệu trả về từ API.
- Viết Test Scripts bằng JavaScript.
- Tự động kiểm tra kết quả của API.
- Kiểm thử trường hợp thành công và trường hợp API trả về lỗi.
Thông qua bài thực hành, em hiểu rõ hơn về cách kiểm thử API và cách sử dụng Postman để hỗ trợ quá trình phát triển và kiểm thử phần mềm.
Kết quả thực hiện gồm 6 Test Case với 12 kiểm thử tự động, trong đó 12/12 Test đều PASS, đạt tỷ lệ thành công 100%.
API được sử dụng trong bài là JSONPlaceholder, một REST API giả lập phục vụ mục đích học tập và kiểm thử. Các thao tác POST, PUT và DELETE được sử dụng để kiểm tra Response của API.
