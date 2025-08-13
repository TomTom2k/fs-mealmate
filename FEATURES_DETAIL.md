# MealMate - Chi tiết tính năng và cách hoạt động

## 📋 Tổng quan dự án

MealMate là một ứng dụng web giúp người dùng quản lý thực đơn cá nhân, tìm kiếm công thức nấu ăn và lên kế hoạch bữa ăn hàng ngày. Ứng dụng được xây dựng theo kiến trúc monorepo với frontend Next.js và backend NestJS.

---

## 🔐 1. Hệ thống xác thực (Authentication)

### Chức năng chính:

- **Đăng ký tài khoản**: Người dùng tạo tài khoản mới với email và mật khẩu
- **Đăng nhập**: Xác thực thông tin đăng nhập và cấp token JWT
- **Quản lý phiên đăng nhập**: Lưu trữ và làm mới token tự động
- **Đăng xuất**: Hủy bỏ phiên đăng nhập hiện tại

### Cách hoạt động:

1. **Đăng ký**:

   - Người dùng nhập email, mật khẩu và xác nhận mật khẩu
   - Hệ thống kiểm tra email chưa được sử dụng
   - Mã hóa mật khẩu bằng bcrypt
   - Tạo user record trong database
   - Gửi email xác nhận (tùy chọn)

2. **Đăng nhập**:

   - Người dùng nhập email và mật khẩu
   - Hệ thống xác thực thông tin với database
   - Tạo JWT token với thời hạn 24 giờ
   - Lưu token vào localStorage/cookies
   - Chuyển hướng đến trang chính

3. **Bảo mật**:
   - JWT token được mã hóa với secret key
   - Token được gửi trong header Authorization cho mọi API call
   - Middleware xác thực token trước khi xử lý request
   - Refresh token để duy trì phiên đăng nhập

---

## 🍳 2. Quản lý công thức nấu ăn (Recipe Management)

### Chức năng chính:

- **Tìm kiếm công thức**: Theo tên món, nguyên liệu, thời gian nấu
- **Xem chi tiết công thức**: Thông tin đầy đủ về món ăn
- **Quản lý món yêu thích**: Lưu và xem các món đã bookmark
- **Phân loại món ăn**: Theo loại món, độ khó, thời gian nấu

### Cách hoạt động:

#### 2.1 Tìm kiếm công thức

1. **Tìm kiếm cơ bản**:

   - Người dùng nhập từ khóa vào ô tìm kiếm
   - Hệ thống tìm kiếm trong database theo:
     - Tên món ăn (LIKE query)
     - Mô tả món ăn
     - Tên nguyên liệu
   - Kết quả được sắp xếp theo độ phù hợp

2. **Tìm kiếm nâng cao**:
   - Lọc theo thời gian nấu (15 phút, 30 phút, 1 giờ...)
   - Lọc theo độ khó (Dễ, Trung bình, Khó)
   - Lọc theo loại món (Món chính, Món phụ, Tráng miệng)
   - Lọc theo chế độ ăn (Chay, Mặn, Keto, Eat clean...)

#### 2.2 Chi tiết công thức

1. **Thông tin cơ bản**:

   - Tên món ăn và hình ảnh
   - Thời gian chuẩn bị và nấu
   - Số khẩu phần
   - Độ khó và đánh giá từ cộng đồng

2. **Nguyên liệu**:

   - Danh sách nguyên liệu với số lượng cụ thể
   - Đơn vị đo lường (gram, ml, cái, quả...)
   - Ghi chú về nguyên liệu (tùy chọn, thay thế được...)

3. **Cách làm**:

   - Các bước nấu được đánh số thứ tự
   - Hình ảnh minh họa cho từng bước
   - Thời gian ước tính cho mỗi bước
   - Mẹo và lưu ý quan trọng

4. **Thông tin dinh dưỡng**:
   - Calories, protein, carbs, fat
   - Vitamin và khoáng chất chính
   - Thông tin về gluten, lactose...

#### 2.3 Quản lý món yêu thích

1. **Thêm vào yêu thích**:

   - Nút "Yêu thích" trên mỗi công thức
   - Lưu vào bảng favorites với user_id và recipe_id
   - Hiển thị trạng thái đã yêu thích

2. **Trang món yêu thích**:
   - Danh sách tất cả món đã bookmark
   - Sắp xếp theo thời gian thêm vào
   - Tìm kiếm trong danh sách yêu thích
   - Xóa khỏi danh sách yêu thích

---

## 📅 3. Lập kế hoạch bữa ăn (Meal Planning)

### Chức năng chính:

- **Tạo kế hoạch bữa ăn**: Cho từng ngày trong tuần
- **Quản lý thực đơn**: Thêm, xóa, thay đổi món ăn
- **Xem lịch bữa ăn**: Giao diện calendar view
- **Tính toán dinh dưỡng**: Tổng calories và chất dinh dưỡng

### Cách hoạt động:

#### 3.1 Tạo kế hoạch bữa ăn

1. **Chọn thời gian**:

   - Chọn ngày cụ thể hoặc khoảng thời gian
   - Mặc định hiển thị tuần hiện tại
   - Có thể xem theo tháng hoặc quý

2. **Thêm món ăn**:

   - Tìm kiếm công thức từ database
   - Chọn bữa ăn (Sáng, Trưa, Tối, Ăn vặt)
   - Chọn số khẩu phần
   - Thêm ghi chú cá nhân

3. **Quản lý thực đơn**:
   - Kéo thả để sắp xếp thứ tự món ăn
   - Copy món ăn sang ngày khác
   - Xóa món ăn khỏi kế hoạch
   - Thay thế món ăn bằng món khác

#### 3.2 Giao diện lập kế hoạch

1. **Calendar View**:

   - Hiển thị theo dạng lịch tuần/tháng
   - Mỗi ngày hiển thị các bữa ăn
   - Màu sắc phân biệt loại bữa ăn
   - Icon hiển thị trạng thái (đã nấu, chưa nấu)

2. **List View**:
   - Danh sách món ăn theo thứ tự thời gian
   - Nhóm theo ngày và bữa ăn
   - Tìm kiếm và lọc trong kế hoạch
   - Export kế hoạch ra PDF/Excel

#### 3.3 Tính toán dinh dưỡng

1. **Tổng hợp dinh dưỡng**:

   - Tính tổng calories cho mỗi ngày
   - Phân tích macro nutrients (protein, carbs, fat)
   - So sánh với mục tiêu dinh dưỡng cá nhân
   - Cảnh báo khi vượt quá giới hạn

2. **Báo cáo dinh dưỡng**:
   - Biểu đồ dinh dưỡng theo tuần/tháng
   - Xu hướng ăn uống theo thời gian
   - Gợi ý điều chỉnh chế độ ăn

---

## 🔍 4. Tìm kiếm và lọc nâng cao

### Chức năng chính:

- **Tìm kiếm thông minh**: Sử dụng Elasticsearch hoặc full-text search
- **Lọc đa tiêu chí**: Kết hợp nhiều điều kiện tìm kiếm
- **Gợi ý tìm kiếm**: Auto-complete và gợi ý từ khóa
- **Lịch sử tìm kiếm**: Lưu và gợi ý các tìm kiếm trước đó

### Cách hoạt động:

#### 4.1 Tìm kiếm thông minh

1. **Full-text search**:

   - Tìm kiếm trong tên món, mô tả, nguyên liệu
   - Hỗ trợ tìm kiếm tiếng Việt có dấu
   - Tìm kiếm gần đúng (fuzzy search)
   - Sắp xếp kết quả theo độ phù hợp

2. **Auto-complete**:
   - Gợi ý từ khóa khi người dùng gõ
   - Dựa trên lịch sử tìm kiếm và độ phổ biến
   - Hiển thị số lượng kết quả cho mỗi gợi ý

#### 4.2 Lọc đa tiêu chí

1. **Bộ lọc cơ bản**:

   - Thời gian nấu: 15 phút, 30 phút, 1 giờ, 2 giờ+
   - Độ khó: Dễ, Trung bình, Khó
   - Loại món: Món chính, Món phụ, Tráng miệng, Nước uống

2. **Bộ lọc nâng cao**:

   - Chế độ ăn: Chay, Mặn, Keto, Low-carb, Gluten-free
   - Nguyên liệu chính: Thịt, cá, rau, trái cây, ngũ cốc
   - Phương pháp nấu: Luộc, xào, nướng, hấp, chiên
   - Xuất xứ: Việt Nam, Châu Á, Châu Âu, Châu Mỹ

3. **Kết hợp bộ lọc**:
   - Sử dụng boolean logic (AND, OR, NOT)
   - Lưu bộ lọc yêu thích để sử dụng lại
   - Reset tất cả bộ lọc về mặc định

---

## 📊 5. Thống kê và báo cáo

### Chức năng chính:

- **Thống kê cá nhân**: Số món đã nấu, thời gian nấu
- **Báo cáo dinh dưỡng**: Phân tích chế độ ăn theo thời gian
- **Xu hướng ăn uống**: Biểu đồ và phân tích thống kê
- **Mục tiêu dinh dưỡng**: Theo dõi và đánh giá tiến độ

### Cách hoạt động:

#### 5.1 Thống kê cá nhân

1. **Số liệu cơ bản**:

   - Tổng số món đã nấu trong tháng
   - Thời gian trung bình nấu mỗi món
   - Số món yêu thích đã lưu
   - Tỷ lệ hoàn thành kế hoạch bữa ăn

2. **Phân tích theo thời gian**:
   - Biểu đồ món ăn theo ngày trong tuần
   - Xu hướng nấu ăn theo tháng
   - So sánh với các tháng trước

#### 5.2 Báo cáo dinh dưỡng

1. **Phân tích macro nutrients**:

   - Biểu đồ tròn hiển thị tỷ lệ protein, carbs, fat
   - So sánh với khuyến nghị dinh dưỡng
   - Cảnh báo khi mất cân bằng dinh dưỡng

2. **Theo dõi calories**:
   - Biểu đồ calories theo ngày
   - Đường mục tiêu calories
   - Phân tích calories theo bữa ăn

---

## 🔧 6. Cài đặt và tùy chỉnh

### Chức năng chính:

- **Hồ sơ cá nhân**: Thông tin cá nhân và sở thích
- **Cài đặt dinh dưỡng**: Mục tiêu calories và macro nutrients
- **Tùy chỉnh giao diện**: Theme, ngôn ngữ, đơn vị đo lường
- **Thông báo**: Cài đặt nhắc nhở và thông báo

### Cách hoạt động:

#### 6.1 Hồ sơ cá nhân

1. **Thông tin cơ bản**:

   - Họ tên, email, số điện thoại
   - Ngày sinh, giới tính, chiều cao, cân nặng
   - Mức độ hoạt động thể chất
   - Mục tiêu (giảm cân, tăng cân, duy trì)

2. **Sở thích ăn uống**:
   - Chế độ ăn ưa thích
   - Thực phẩm dị ứng hoặc không thích
   - Khẩu vị (cay, chua, ngọt, mặn)
   - Thời gian ăn uống thường xuyên

#### 6.2 Cài đặt dinh dưỡng

1. **Mục tiêu calories**:

   - Tính toán BMR (Basal Metabolic Rate)
   - Điều chỉnh theo mục tiêu và hoạt động
   - Phân bổ calories theo bữa ăn

2. **Macro nutrients**:
   - Tỷ lệ protein, carbs, fat
   - Số gram cụ thể cho mỗi chất
   - Điều chỉnh theo chế độ ăn đặc biệt

---

## 📱 7. Giao diện người dùng

### Thiết kế:

- **Responsive design**: Tương thích với mọi thiết bị
- **Material Design**: Sử dụng Google Material Design principles
- **Dark/Light mode**: Hỗ trợ chế độ tối và sáng
- **Accessibility**: Tuân thủ WCAG guidelines

### Cấu trúc trang:

1. **Header**: Logo, navigation menu, search bar, user profile
2. **Sidebar**: Menu chính, quick actions, recent recipes
3. **Main content**: Nội dung chính của từng trang
4. **Footer**: Links, social media, contact information

---

## 🚀 8. Kiến trúc kỹ thuật

### Frontend (Next.js):

- **Pages**: Sử dụng App Router của Next.js 13+
- **Components**: React components với TypeScript
- **State Management**: Zustand hoặc Redux Toolkit
- **Styling**: Tailwind CSS với custom components
- **API Integration**: Apollo Client cho GraphQL

### Backend (NestJS):

- **Modules**: Auth, Recipe, MealPlan, User
- **GraphQL**: Apollo Server với code-first approach
- **Database**: PostgreSQL với TypeORM
- **Authentication**: JWT với Passport.js
- **Validation**: Class-validator và class-transformer

### Database Schema:

1. **Users**: Thông tin người dùng và cài đặt
2. **Recipes**: Công thức nấu ăn và metadata
3. **Ingredients**: Nguyên liệu và thông tin dinh dưỡng
4. **RecipeIngredients**: Quan hệ many-to-many giữa recipe và ingredient
5. **MealPlans**: Kế hoạch bữa ăn theo ngày
6. **Favorites**: Món ăn yêu thích của người dùng

---

## 🔄 9. Luồng hoạt động chính

### Luồng tìm kiếm công thức:

1. Người dùng nhập từ khóa tìm kiếm
2. Frontend gửi GraphQL query đến backend
3. Backend xử lý tìm kiếm trong database
4. Trả về kết quả với pagination
5. Frontend hiển thị kết quả và cho phép lọc

### Luồng lập kế hoạch bữa ăn:

1. Người dùng chọn ngày và bữa ăn
2. Tìm kiếm và chọn công thức phù hợp
3. Thêm vào kế hoạch với số khẩu phần
4. Lưu vào database thông qua GraphQL mutation
5. Cập nhật giao diện và tính toán dinh dưỡng

### Luồng quản lý món yêu thích:

1. Người dùng click nút "Yêu thích" trên công thức
2. Frontend gửi GraphQL mutation
3. Backend thêm/ xóa record trong bảng favorites
4. Cập nhật trạng thái UI và thông báo

---

## 📈 10. Hướng phát triển tương lai

### Giai đoạn 2 (Tháng 3-4):

- **AI gợi ý**: Machine learning để gợi ý món ăn
- **Cộng đồng**: Chia sẻ công thức và đánh giá
- **Mobile app**: React Native app cho iOS/Android

### Giai đoạn 3 (Tháng 5-6):

- **Tích hợp siêu thị**: API kết nối với siêu thị online
- **Meal kit delivery**: Dịch vụ giao nguyên liệu tận nhà
- **Social features**: Follow người dùng, tạo nhóm nấu ăn

### Giai đoạn 4 (Tháng 7-8):

- **Voice assistant**: Hỗ trợ tìm kiếm bằng giọng nói
- **AR cooking guide**: Hướng dẫn nấu ăn với AR
- **IoT integration**: Kết nối với thiết bị nhà bếp thông minh

---

## 🧪 11. Testing và Quality Assurance

### Testing Strategy:

- **Unit tests**: Jest cho frontend và backend
- **Integration tests**: Testing API endpoints
- **E2E tests**: Playwright cho user flows
- **Performance tests**: Lighthouse và WebPageTest

### Code Quality:

- **ESLint**: Code style và best practices
- **Prettier**: Code formatting
- **Husky**: Pre-commit hooks
- **TypeScript**: Type safety và IntelliSense

---

## 📚 12. Tài liệu và hỗ trợ

### API Documentation:

- **GraphQL Schema**: Auto-generated từ code
- **Postman Collection**: API testing examples
- **Swagger/OpenAPI**: REST endpoints (nếu có)

### User Guide:

- **Getting Started**: Hướng dẫn sử dụng cơ bản
- **FAQ**: Câu hỏi thường gặp
- **Video tutorials**: Hướng dẫn bằng video
- **Support**: Email và live chat hỗ trợ

---

_Tài liệu này sẽ được cập nhật liên tục trong quá trình phát triển dự án._
