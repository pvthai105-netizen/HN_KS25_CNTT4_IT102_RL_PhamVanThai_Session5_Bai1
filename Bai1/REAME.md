## 1. Phân tích lỗi & Lập Test Cases

### Phân tích lỗi

Mã nguồn sử dụng mảng:

```c
int queue_numbers[4] = {1001, 1002, 1003, 1004};
```

Mảng có 4 phần tử nên chỉ có các index từ `0` đến `3`.

Lỗi xảy ra tại dòng:

```c
queue_numbers[patient_position] = new_queue_number;
```

Khi `patient_position = 4`, chương trình thực hiện:

```c
queue_numbers[4] = 1099;
```

Tuy nhiên `queue_numbers[4]` không tồn tại. Đây là lỗi **truy cập vượt giới hạn mảng (Array Out of Bounds)**, dẫn đến **Undefined Behavior**.

Về nghiệp vụ, nếu muốn cập nhật bệnh nhân ở vị trí thứ 4 thì phải sử dụng index `3`.

### Test Case 1: Cập nhật bệnh nhân vị trí thứ 4

* **Trường hợp kiểm thử:** Cập nhật mã số cho bệnh nhân vị trí thứ 4.
* **Dữ liệu đầu vào:** `patient_position = 4`, `new_queue_number = 1099`.
* **Kết quả sai thực tế:** Chương trình truy cập `queue_numbers[4]`, vượt khỏi phạm vi mảng. Giá trị `1099` không được cập nhật vào bệnh nhân thứ 4 và có thể gây Undefined Behavior.
* **Kết quả đúng mong đợi:** Mã số của bệnh nhân thứ 4 được cập nhật thành `1099`. Do mảng bắt đầu từ index `0`, cần sử dụng `queue_numbers[3]`.

### Test Case 2: Cập nhật bệnh nhân vị trí thứ 2

* **Trường hợp kiểm thử:** Cập nhật mã số cho bệnh nhân vị trí thứ 2.
* **Dữ liệu đầu vào:** `patient_position = 1`, `new_queue_number = 1099`.
* **Kết quả sai thực tế:** Nếu hiểu `patient_position` là vị trí bệnh nhân, chương trình sẽ cập nhật `queue_numbers[1]`, tức bệnh nhân thứ 2. Trường hợp này cho thấy cần phân biệt giữa vị trí nghiệp vụ và index của mảng.
* **Kết quả đúng mong đợi:** Bệnh nhân thứ 2 được cập nhật thành `1099`. Nếu `patient_position` biểu diễn vị trí bắt đầu từ `1`, cần sử dụng `queue_numbers[patient_position - 1]`.
