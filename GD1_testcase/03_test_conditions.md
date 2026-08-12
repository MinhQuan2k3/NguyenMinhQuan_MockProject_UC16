# Test Conditions – Final Reviewed Baseline

## 1. Status

**Human Review 2:** PASS WITH CORRECTIONS  
**Approved conditions:** 23  
**Raw Node 5 conditions rejected:** 2  
**Purpose:** Controlled input/baseline for final Test Case review.

## 2. Approved Conditions

| ID | Test Condition | Type | Authoritative Trace |
|---|---|---|---|
| C20-01 | Edit từ Interview Schedule List mở/chuyển tới Edit của schedule được chọn và tải đúng schedule. | Pos | UC20 Basic Flow Steps 1–2 |
| C20-02 | Edit screen hiển thị dữ liệu hiện tại của schedule được chọn. | Pos | UC20 Basic Flow Step 2; Screen Description |
| C20-03 | Dữ liệu trên Edit screen không bị thay thế bởi dữ liệu schedule khác hoặc sai mapping. | Neg | UC20 Basic Flow Step 2; Screen Description |
| C20-04 | Edit từ Interview Schedule Detail mở Edit tương ứng. | Pos | UC20 Alternative Flow A1 |
| C20-05 | User đã đăng nhập và có appropriate permission có thể thực hiện Edit. | Pos | UC20 Overview – Pre-condition/Actor |
| C20-06 | Permission kiểm soát quyền truy cập Edit; không suy diễn role/permission matrix. | Neg | UC20 Overview – Pre-condition/Actor |
| C20-07 | Edit screen hiển thị đầy đủ components được mô tả. | Pos | UC20 Screen Description |
| C20-08 | Components không bị thiếu/sai control so với Screen Description. | Neg | UC20 Screen Description |
| C20-09 | Các field Schedule Title, Interviewer, Schedule, Schedule From/To, Location và Recruiter Owner cho phép chỉnh sửa theo mô tả. | Pos | UC20 Screen Description refs 4–11 |
| C20-10 | Các field editable không bị khóa trái mô tả. | Neg | UC20 Screen Description refs 4–11 |
| C20-11 | Assign me được hiển thị. | Pos | UC20 Screen Description ref 12 |
| C20-12 | Assign me đúng loại control; persistence sau Submit không được giả định. | Neg | UC20 Screen Description ref 12 |
| C20-13 | Khi required fields hoàn tất, không phát sinh ME002 do thiếu dữ liệu. | Pos | BRL-20-01; ME002 |
| C20-14 | Thiếu required field → ME002 “Required field”. | Neg | BRL-20-01; ME002 |
| C20-15 | Chỉ Job có Status = Open được load/đưa vào danh sách lựa chọn. | Pos | BRL-20-03 |
| C20-16 | Job có Status khác Open không được load/đưa vào danh sách lựa chọn. | Neg | BRL-20-03 |
| C20-17 | Status hiện tại hiển thị đúng. | Pos | Screen Description ref 13 |
| C20-18 | Result hiện tại hiển thị đúng. | Pos | Screen Description ref 14 |
| C20-19 | Status không cho phép chỉnh sửa. | Neg | Screen Description ref 13 |
| C20-20 | Result cho phép chỉnh sửa; không suy diễn allowed values/validation. | Pos | Screen Description ref 14 |
| C20-21 | Submit, Cancel và Cancel Schedule được hiển thị. | Pos | Screen Description refs 15–17 |
| C20-22 | Submit thành công → ME014. | Pos | Screen Description ref 15; ME014 |
| C20-23 | Submit thất bại → ME013. | Neg | Screen Description ref 15; ME013 |

## 3. Excluded / Unresolved

Không tạo Test Condition bắt buộc cho:

- invalid/missing schedule;
- load failure;
- authentication failure behavior;
- detailed permission matrix;
- exact required-field list;
- Result values/validation;
- date/time validation;
- Cancel outcome;
- Cancel Schedule outcome;
- Assign Me persistence;
- concurrency.

## 4. Traceability Control

Chỉ dùng requirement/message/reference thực sự có trong UC. Các `AC-20-xx` và `BR-20-xx` do AI tự sinh không được coi là authoritative.

Đặc biệt:

- `BRL-20-01` = required-field rule.
- `BRL-20-03` = **Job + Open status**.
- `ME002` = required-field validation message.
- `ME013` = failed update message.
- `ME014` = successful update message.

## 5. Final Decision

**Approved baseline for final Test Case review.**
