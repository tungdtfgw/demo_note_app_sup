# PRD: MyNotes

## Tổng quan

MyNotes là ứng dụng ghi chú trên điện thoại, xây dựng bằng React Native + Expo, sử dụng Supabase làm backend. Người dùng đăng nhập bằng email magic link và quản lý ghi chú cá nhân trên nhiều thiết bị.

## Đối tượng sử dụng

Bất kỳ ai cần một ứng dụng ghi chú đơn giản, đồng bộ nhiều thiết bị, không cần nhớ mật khẩu.

## Tính năng chính

### 1. Xác thực (Magic Link)

- Đăng nhập bằng email — Supabase gửi magic link, không cần mật khẩu.
- Email lần đầu = tự động tạo tài khoản.
- Lưu phiên đăng nhập trên máy — người dùng không cần đăng nhập lại cho đến khi tự đăng xuất.
- Nút đăng xuất ở khu vực cài đặt/hồ sơ.
- Mỗi người dùng chỉ thấy ghi chú của mình.

### 2. Danh sách ghi chú (Màn hình chính)

- Hiển thị tất cả ghi chú, sắp xếp: ghim lên đầu, sau đó theo ngày sửa đổi (mới nhất trước).
- Mỗi mục hiển thị: biểu tượng ghim, tiêu đề (hoặc dòng đầu nếu không có tiêu đề), xem trước nội dung, nhãn danh mục, ngày sửa đổi.
- Trạng thái trống: thông báo thân thiện + nút tạo ghi chú đầu tiên.
- Kéo xuống để làm mới dữ liệu từ Supabase.

### 3. Tạo / Sửa ghi chú

- Nhấn "+" để tạo ghi chú mới, nhấn vào ghi chú bất kỳ để sửa.
- Các trường: tiêu đề (tuỳ chọn, một dòng), nội dung (nhiều dòng, văn bản thuần), danh mục (bộ chọn, tuỳ chọn).
- Tự động lưu mỗi khi ngừng gõ (debounce 1 giây) — không có nút lưu thủ công.
- Hiển thị thời gian "đã lưu lần cuối" ở cuối màn hình.

### 4. Xoá ghi chú (Xoá mềm + Thùng rác)

- Vuốt trái trên ghi chú trong danh sách để hiện nút xoá.
- Ghi chú bị xoá chuyển vào Thùng rác — không bị xoá vĩnh viễn ngay.
- Màn hình Thùng rác hiển thị các ghi chú đã xoá kèm ngày xoá.
- Từ Thùng rác: khôi phục ghi chú hoặc xoá vĩnh viễn.
- Ghi chú trong Thùng rác tự động bị xoá vĩnh viễn sau 30 ngày.

### 5. Ghim ghi chú

- Nhấn giữ hoặc nhấn biểu tượng ghim trên ghi chú để bật/tắt ghim.
- Ghi chú được ghim luôn hiển thị ở đầu danh sách, phía trên các ghi chú chưa ghim.
- Trong nhóm ghim: sắp xếp theo ngày sửa đổi (mới nhất trước).
- Trạng thái ghim được đồng bộ — giữ nguyên trên các thiết bị.

### 6. Danh mục

- Mỗi ghi chú thuộc một danh mục (hoặc không có).
- Người dùng tự quản lý danh mục: tạo, đổi tên, xoá.
- Bộ chọn danh mục trong màn hình chỉnh sửa ghi chú.
- Lọc ghi chú theo danh mục trên màn hình chính.
- Xoá danh mục → các ghi chú thuộc danh mục đó chuyển thành "chưa phân loại", không bị xoá.

### 7. Tìm kiếm

- Thanh tìm kiếm ở đầu màn hình chính.
- Lọc ghi chú theo tiêu đề và nội dung (không phân biệt hoa thường).
- Tìm kiếm kết hợp với bộ lọc danh mục (nếu đang lọc).
- Kết quả cập nhật khi người dùng gõ (debounce 300ms).
- Tìm kiếm không bao gồm ghi chú trong Thùng rác.

## Ngoài phạm vi (v1)

- Không hỗ trợ văn bản phong phú, markdown, hoặc đính kèm tệp
- Không đồng bộ thời gian thực (chỉ kéo xuống để làm mới)
- Không hoạt động ngoại tuyến với xử lý xung đột
- Không chia sẻ hoặc cộng tác
- Không chuyển đổi giao diện sáng/tối (theo cài đặt hệ thống)
- Không sắp xếp lại ghi chú ngoài ghim + sắp xếp theo ngày
