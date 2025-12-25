# NOW CHALLENGE - Hệ thống Quản lý Đặt Xe Công Nghệ MinRide

## 1. Giới thiệu

MinRide là hệ thống quản lý đặt xe thông qua giao diện dòng lệnh (console),
được xây dựng như một đồ án thực hành cho môn học **Cấu trúc Dữ liệu và Giải thuật**.

Chương trình mô phỏng các nghiệp vụ cơ bản của một hệ thống gọi xe, bao gồm
quản lý **Tài xế**, **Khách hàng** và **Chuyến đi**. Trọng tâm của đồ án là
việc lựa chọn và cài đặt các cấu trúc dữ liệu và giải thuật phù hợp nhằm
tối ưu hiệu năng tìm kiếm, sắp xếp và quản lý dữ liệu.

Dữ liệu ban đầu được nạp sẵn từ các file văn bản. Sau khi khởi động,
người dùng có thể tiếp tục thao tác thông qua hệ thống menu.

---

## 2. Yêu cầu hệ thống

- Hệ điều hành: Windows / Linux / macOS  
- Ngôn ngữ lập trình: C++  
- Trình biên dịch: g++ (Chuẩn C++11 trở lên)

---

## 3. Cấu trúc thư mục

```
MinRide/
│── MinRide.cpp          // Mã nguồn chính, chứa toàn bộ logic và CTDL
│── taixe.txt            // Dữ liệu tài xế (nạp tự động)
│── khachhang.txt        // Dữ liệu khách hàng (nạp tự động)
│── chuyendi.txt         // Dữ liệu chuyến đi (nạp tự động)
│── README.md            // Tài liệu hướng dẫn
```

---

## 4. Dữ liệu đầu vào mẫu

Hệ thống tự động đọc dữ liệu từ các file văn bản khi khởi động.

### 4.1. Tài xế – `taixe.txt`

```
ID, Tên, Rating, X, Y
```

Ví dụ:
```
1, An, 4.8, 2.5, 5.3
```

---

### 4.2. Khách hàng – `khachhang.txt`

```
ID, Tên, Khu vực, X, Y
```

Ví dụ:
```
1, Hoa, Q1, 3, 3
```

---

### 4.3. Chuyến đi – `chuyendi.txt`

```
ID chuyến, ID tài xế, ID khách hàng, Timestamp, Quãng đường, Giá tiền
```

Ví dụ:
```
3,101,203,1700001200,2.8,22000
```

---

## 5. Biên dịch chương trình

Mở Terminal hoặc Command Prompt tại thư mục dự án và chạy:

```
g++ MinRide.cpp -o MinRide
```

---

## 6. Chạy chương trình

Windows:
```
MinRide.exe
```

Linux / macOS:
```
./MinRide
```

---

## 7. Luồng hoạt động của chương trình

1. Đọc và phân tích dữ liệu từ các file `.txt`  
2. Lưu trữ dữ liệu vào các cấu trúc dữ liệu trong bộ nhớ  
3. Hiển thị menu chính (chia theo nhóm Tài xế, Khách hàng, Chuyến đi)  
4. Cho phép người dùng thực hiện các chức năng:
   - Thêm, xóa, tìm kiếm tài xế và khách hàng
   - Quản lý và tra cứu lịch sử chuyến đi
   - Tìm tài xế trong bán kính xác định so với vị trí khách hàng
   - Đề xuất tài xế phù hợp dựa trên khoảng cách và điểm đánh giá
   - Hoàn tác (Undo) và làm lại (Redo) các thao tác quản lý dữ liệu

---

## 8. Cấu trúc dữ liệu và giải thuật sử dụng

- **Cây AVL (tự cài đặt):**  
  Chương trình định nghĩa cấu trúc `NutAVL` và cài đặt đầy đủ các phép xoay
  (xoay trái, xoay phải, xoay kép) cùng hàm tính độ cân bằng để duy trì tính
  tự cân bằng của cây.  
  Cây AVL được sử dụng trong các module quản lý **Tài xế**, **Khách hàng**
  và **Chuyến đi**, giúp các thao tác tìm kiếm, thêm và xóa theo ID đạt
  hiệu năng tối ưu với độ phức tạp $O(\log n)$.

- **Quick Sort (tự cài đặt):**  
  Thuật toán Quick Sort được cài đặt thủ công dựa trên kỹ thuật phân hoạch
  (partitioning), không phụ thuộc vào `std::sort`.  
  Thuật toán này được sử dụng để sắp xếp danh sách tài xế theo **điểm đánh giá
  (Rating)** hoặc theo **khoảng cách đến khách hàng**, phục vụ nghiệp vụ
  tìm kiếm và đề xuất tài xế phù hợp.

- **Ngăn xếp (`std::stack`):**  
  Dùng để cài đặt hệ thống **Undo / Redo**, lưu trữ lịch sử các thao tác quản lý
  dữ liệu, cho phép người dùng hoàn tác hoặc thực hiện lại các thao tác trước đó.

- **Bảng ánh xạ (`std::map`):**  
  Sử dụng như một cấu trúc chỉ mục (indexing) để quản lý và truy xuất nhanh
  danh sách khách hàng theo khu vực (Quận).

- **Tính toán hình học:**  
  Áp dụng công thức khoảng cách Euclid giữa các tọa độ $(X, Y)$ để xác định
  khoảng cách giữa tài xế và khách hàng.

- **Xử lý luồng dữ liệu (Stream Processing):**  
  Sử dụng `fstream` và `stringstream` để đọc, phân tích và nạp dữ liệu
  từ các file văn bản khi chương trình khởi động.

---

## 9. Lưu ý

- Chương trình hoạt động hoàn toàn trên giao diện dòng lệnh  
- Dữ liệu được xử lý trong bộ nhớ sau khi nạp từ file  
- Trọng tâm đồ án là áp dụng **Cấu trúc Dữ liệu & Giải thuật**, không tập trung giao diện  

---

## 10. Kết luận

MinRide là đồ án thể hiện rõ việc áp dụng các **cấu trúc dữ liệu và giải thuật**
trong bài toán quản lý đặt xe.

Sự kết hợp giữa cây AVL, Quick Sort, Map và Stack giúp hệ thống hoạt động hiệu quả,
dễ mở rộng và đáp ứng tốt yêu cầu của môn học.

---

## 11. Ví dụ thao tác mẫu

- Khởi động chương trình → nạp dữ liệu ban đầu  
- Chọn chức năng tìm tài xế phù hợp  
- Nhập ID khách hàng và bán kính tìm kiếm  
- Hệ thống hiển thị danh sách tài xế thỏa điều kiện  
- Chọn chức năng Undo để hoàn tác thao tác vừa thực hiện
