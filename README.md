# 🐋 Interactive Whale

<div align="center">

### Một chú cá voi sát thủ, sống động theo từng chuyển động chuột.

Mô phỏng tương tác toàn màn hình được dựng bằng SVG — tối giản, trực quan và sẵn sàng chạy ngay trên trình duyệt.

![HTML5](https://img.shields.io/badge/HTML5-static-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-layout-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-interactive-F7DF1E?style=for-the-badge&logo=javascript&logoColor=111111)
![No build](https://img.shields.io/badge/build-none-22C55E?style=for-the-badge)

**Tác giả: Lê Phú An**

</div>

---

## ✨ Giới thiệu

**Interactive Whale** là một trải nghiệm đồ họa tương tác chạy trực tiếp trong trình duyệt. Trang hiển thị hình cá voi sát thủ được tạo từ nhiều lớp vector SVG; khi di chuyển con trỏ, các lớp chuyển động bám theo với độ trễ và hiệu ứng easing, tạo cảm giác hình ảnh có chiều sâu và đang chuyển động.

Đây là một trang trình diễn hình ảnh đơn trang: không có menu, nội dung bài viết, biểu mẫu hay backend. Mở trang lên là có thể tương tác ngay.

## 📑 Mục lục

- [Trải nghiệm trên trang](#-trải-nghiệm-trên-trang)
- [Cách chạy](#-cách-chạy)
- [Cách tương tác](#-cách-tương-tác)
- [Công nghệ và cách hoạt động](#-công-nghệ-và-cách-hoạt-động)
- [Cấu trúc dự án](#-cấu-trúc-dự-án)
- [Tùy chỉnh](#-tùy-chỉnh)
- [Tương thích và giới hạn](#-tương-thích-và-giới-hạn)
- [Ghi công và tác giả](#-ghi-công-và-tác-giả)

## 🎨 Trải nghiệm trên trang

- **Đồ họa cá voi sát thủ:** các đường path SVG được xếp thành nhiều lớp, phối gradient và sắc độ đen, xám, trắng.
- **Chuyển động theo con trỏ:** hình ảnh dịch chuyển hướng về vị trí chuột, với các lớp phản hồi lần lượt thay vì di chuyển đồng loạt.
- **Hiển thị toàn màn hình:** vùng đồ họa chiếm gần trọn chiều rộng và chiều cao cửa sổ trình duyệt.
- **Không cần cài đặt hay biên dịch:** dự án là trang web tĩnh với các tệp nằm cạnh nhau.

## 🚀 Cách chạy

### Mở trực tiếp

1. Tải hoặc sao chép thư mục dự án về máy.
2. Mở `interactive-whale.html` bằng trình duyệt hiện đại.
3. Di chuyển chuột trong vùng trang để xem hiệu ứng.

### Chạy bằng máy chủ tĩnh

Nếu bạn đang ở trong thư mục chứa các tệp của dự án, có thể dùng máy chủ HTTP tích hợp của Python 3:

```bash
python -m http.server 8000
```

Sau đó mở `http://localhost:8000` trong trình duyệt. Không cần cài thêm package; dự án không có bước build, cấu hình môi trường hay kết nối dịch vụ bên ngoài.

## 🖱️ Cách tương tác

| Thao tác | Kết quả |
|---|---|
| Di chuyển chuột | Các lớp của cá voi dịch chuyển theo con trỏ với độ trễ tạo chiều sâu |
| Đưa chuột tới vị trí khác | Hình tiếp tục bám theo và giảm tốc dần khi tiến gần mục tiêu |

Trang không có nút điều khiển hoặc trạng thái cần thiết lập; hiệu ứng bắt đầu tự động khi tải trang.

## ⚙️ Công nghệ và cách hoạt động

- **HTML** cung cấp vùng chứa `#whale` và nạp stylesheet cùng JavaScript.
- **CSS** đặt trang và vùng chứa phủ gần toàn bộ viewport, không có lề mặc định.
- **JavaScript thuần** theo dõi sự kiện `mousemove`, cập nhật vị trí mục tiêu và dựng SVG trong vùng chứa.
- **SVG** chứa các đường path và gradient tạo nên hình minh họa nhiều lớp.
- Mô phỏng được cập nhật theo nhịp **30 lần mỗi giây**. Mỗi lớp có độ trễ khác nhau; vị trí được điều chỉnh dần về con trỏ, giới hạn bước dịch chuyển để chuyển động mượt hơn.
- Tọa độ đồ họa được thu nhỏ theo tỷ lệ `0.05` khi dựng từng nhóm SVG.
- `jquery.js` đi kèm là **jQuery 2.1.3**. Tệp HTML hiện nạp thư viện này, tuy nhiên logic hiệu ứng trong `interactive-whale.js` sử dụng API trình duyệt thuần.

## 📁 Cấu trúc dự án

```text
44/
├── README.md               # Tài liệu dự án
├── interactive-whale.html  # Trang HTML, vùng hiển thị và thứ tự nạp script
├── interactive-whale.css   # Quy tắc kích thước trang và vùng hiển thị
├── interactive-whale.js    # Dữ liệu SVG và logic chuyển động theo chuột
└── jquery.js               # jQuery 2.1.3 được đóng gói cùng dự án
```

## 🛠️ Tùy chỉnh

Các giá trị điều khiển chuyển động nằm ở phần đầu `interactive-whale.js`:

| Biến | Giá trị hiện tại | Tác dụng |
|---|---:|---|
| `fps` | `30` | Tần suất cập nhật mô phỏng |
| `easy` | `6` | Mức chia khoảng cách để làm mượt chuyển động |
| `maxspeed` | `150` | Giới hạn dịch chuyển mỗi lần cập nhật |
| `delay` | `15` | Hệ số độ trễ giữa các lớp |

Có thể điều chỉnh các giá trị trên để thử cảm giác chuyển động khác nhau. Phần minh họa SVG được khai báo trong mảng `parts`; thay đổi các đường path hoặc gradient tại đây sẽ tác động trực tiếp tới hình ảnh.

## 📱 Tương thích và giới hạn

- Hiệu ứng tương tác hiện được điều khiển bằng chuột (`mousemove`); chưa có xử lý riêng cho cảm ứng hoặc thao tác bàn phím.
- Kích thước viewport được đọc khi khởi tạo; trang chưa có logic cập nhật lại tọa độ khi cửa sổ thay đổi kích thước.
- Đây là demo đồ họa phía trình duyệt, không có API, cơ sở dữ liệu, lưu trữ dữ liệu người dùng hay quy trình kiểm thử/build riêng.
- Tệp JavaScript chứa dữ liệu path SVG dung lượng lớn; khi chỉnh sửa, cần giữ nguyên cấu trúc chuỗi SVG để tránh làm hỏng phần minh họa.

## 🙌 Ghi công và tác giả

- **Tác giả README:** Lê Phú An.
- Tệp HTML hiện có ghi chú ghi công `@diegoleme` cho phần minh họa gốc. Vui lòng giữ lại và tôn trọng ghi công này khi phân phối hoặc chỉnh sửa dự án.
- Thư viện jQuery đi kèm có thông tin bản quyền và giấy phép trong phần đầu của `jquery.js`; tham khảo [jquery.org/license](https://jquery.org/license).

---

<div align="center">

**Được tạo với sự tỉ mỉ bởi Lê Phú An**  
*Một chuyển động nhỏ, một đại dương sống động.*

</div>
