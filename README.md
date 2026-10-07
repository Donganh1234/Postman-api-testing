# BÁO CÁO THỰC HÀNH KIỂM THỬ API BẰNG POSTMAN

## 1. Thông tin bài thực hành

- **Họ và tên:** Ánh Đồng
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
#### Kết quả mong đợi
- HTTP Status Code: 200 OK
- Response trả về một mảng dữ liệu Users.
- Mảng Users có ít nhất một phần tử.
#### Test Script:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response contains users", function () {
    const data = pm.response.json();
    pm.expect(data).to.be.an("array");
    pm.expect(data.length).to.be.greaterThan(0);
});
