# REST API Cơ Bản

## 1. REST dùng danh từ số nhiều cho URL, không dùng động từ

**Đúng.**

Trong REST API, URL nên biểu diễn tài nguyên (resource) nên thường dùng danh từ số nhiều, còn hành động sẽ do HTTP Method quyết định.

### Sai

```http
/getStudents
/createStudent
```

### Đúng

```http
/students
/students/1
```

---

## 2. Ví dụ đúng và sai cho API quản lý sinh viên

### Ví dụ đúng

```http
GET /students
```

Lấy danh sách sinh viên.

```http
DELETE /students/5
```

Xóa sinh viên có `id = 5`.

### Ví dụ sai

```http
GET /getAllStudents
POST /createNewStudent
```

---

## 3. Các phương thức HTTP dùng để làm gì?

| Method | Mục đích chính | Có body không? (thường) |
|----------|----------------|--------------------------|
| GET | Lấy dữ liệu | Không |
| POST | Tạo mới dữ liệu | Có |
| PUT | Cập nhật toàn bộ dữ liệu | Có |
| PATCH | Cập nhật một phần dữ liệu | Có |
| DELETE | Xóa dữ liệu | Thường không |

---

## 4. Phân biệt PUT và PATCH

Giả sử sản phẩm ban đầu:

```json
{
  "id": 1,
  "name": "Bút bi",
  "price": 5000
}
```

### PUT

**Request**

```http
PUT /products/1
```

**Body**

```json
{
  "name": "Bút mực"
}
```

**Kết quả**

```json
{
  "id": 1,
  "name": "Bút mực",
  "price": null
}
```

> PUT thường được hiểu là ghi đè toàn bộ object. Những field không gửi lên có thể bị mất hoặc trở thành `null`.

### PATCH

**Request**

```http
PATCH /products/1
```

**Body**

```json
{
  "name": "Bút mực"
}
```

**Kết quả**

```json
{
  "id": 1,
  "name": "Bút mực",
  "price": 5000
}
```

> PATCH chỉ cập nhật các field được gửi lên, các field còn lại được giữ nguyên.

---

## 5. HTTP Status Codes

| Mã | Ý nghĩa | Tình huống ví dụ |
|-----|----------|------------------|
| 200 | OK – Thành công | Lấy danh sách sinh viên thành công |
| 201 | Created – Tạo mới thành công | Thêm sinh viên mới thành công |
| 204 | No Content – Thành công nhưng không trả dữ liệu | Xóa sinh viên thành công |
| 400 | Bad Request – Request sai dữ liệu | Thiếu field `name` khi tạo sinh viên |
| 404 | Not Found – Không tìm thấy tài nguyên | Không tìm thấy sinh viên `id = 99` |
| 500 | Internal Server Error – Lỗi phía server | Server bị lỗi database hoặc code |