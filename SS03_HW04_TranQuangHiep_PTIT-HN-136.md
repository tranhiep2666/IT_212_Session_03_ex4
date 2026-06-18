# Prompt sinh Đặc tả Yêu cầu Phi Chức năng (NFR) cho Guai-api

Bạn là Senior Solution Architect và Performance Engineer với kinh nghiệm thiết kế hệ thống thương mại điện tử quy mô lớn.

## Bối cảnh hệ thống

Hệ thống Guai-api là backend API phục vụ Shop AI, cung cấp các chức năng:

* Tra cứu danh sách sản phẩm
* Tìm kiếm sản phẩm theo từ khóa
* Xem chi tiết sản phẩm
* Xác thực người dùng bằng JWT
* Kết nối cơ sở dữ liệu MySQL

Hệ thống cần chuẩn bị cho các đợt traffic cao điểm (Flash Sale, Mega Campaign, Black Friday, 11.11, 12.12).

## Nhiệm vụ

Hãy xây dựng phần **Đặc tả Yêu cầu Phi Chức năng (Non-Functional Requirements - NFR)** cho Guai-api.

### Yêu cầu chung

1. Trình bày dưới dạng tài liệu kỹ thuật.

2. Mỗi NFR phải bao gồm:

    * Mục tiêu
    * Chỉ tiêu/KPI định lượng
    * Cách đo lường
    * Giải thích lý do lựa chọn
    * Khuyến nghị triển khai

3. Không đưa ra mô tả chung chung.

4. Tất cả chỉ tiêu phải có giá trị số cụ thể.

5. Giả định hệ thống phục vụ tối thiểu 100.000 người dùng đồng thời.

---

# Phần 1 - Response Time

Phân tích và đề xuất NFR cho các endpoint:

* GET /products
* GET /products/{id}
* GET /search

Yêu cầu:

* Đưa ra chỉ tiêu Response Time tối đa.
* Phân biệt:

    * Average Response Time
    * P95
    * P99
* Đề xuất TPS/RPS mục tiêu.
* Xác định ngưỡng cảnh báo và ngưỡng vi phạm SLA.
* Giải thích cách áp dụng Cache nếu cần.

Kết quả trình bày dưới dạng bảng.

---

# Phần 2 - Hiệu suất MySQL và Indexing Strategy

Phân tích các truy vấn phổ biến:

* Tìm kiếm sản phẩm theo tên
* Tra cứu theo Product ID
* Lọc theo Category
* Lọc theo Brand
* Sắp xếp theo Price
* Sắp xếp theo Created Date

Yêu cầu AI:

1. Xác định nguy cơ Full Table Scan.

2. Đề xuất chiến lược Indexing.

3. Chỉ rõ loại index:

    * Primary Index
    * Composite Index
    * Covering Index
    * Full-text Index (nếu phù hợp)

4. Đề xuất KPI:

    * Query Response Time
    * Database CPU Usage
    * Slow Query Threshold
    * Connection Pool Usage

5. Đưa ra bảng Mapping:

| Query Pattern | Recommended Index | Expected Improvement |

6. Giải thích lý do lựa chọn từng loại Index.

---

# Phần 3 - JWT Authentication & Security

Phân tích luồng:

Client → Guai-api → JWT Validation → Business Logic

Yêu cầu AI đề xuất NFR cho:

### Hiệu năng

* JWT Generation Time
* JWT Validation Time
* Authentication Throughput
* Cache Strategy cho JWT Validation

### Bảo mật

* Thuật toán ký JWT khuyến nghị
* Key Rotation Policy
* Token Expiration Policy
* Refresh Token Policy
* Replay Attack Prevention
* Brute Force Protection
* Rate Limiting

### KPI bảo mật

Yêu cầu đưa ra các chỉ tiêu định lượng như:

* Số lần login thất bại tối đa/phút
* Tần suất rotation key
* Thời gian sống Access Token
* Thời gian sống Refresh Token
* Thời gian phát hiện tấn công

---

# Định dạng đầu ra

Xuất kết quả theo cấu trúc:

1. Executive Summary
2. NFR - Response Time
3. NFR - MySQL Performance & Indexing
4. NFR - JWT Authentication & Security
5. SLA/SLO Summary Table
6. Risk & Recommendation

Tất cả NFR phải ở mức có thể đưa trực tiếp vào tài liệu SRS hoặc SAD của dự án.
