# MealMate - Ứng dụng gợi ý & quản lý thực đơn cá nhân

## 🎯 Mục đích dự án

MealMate giúp người dùng:

- Lên kế hoạch ăn uống hàng ngày/tuần.
- Tìm kiếm món ăn nhanh theo nguyên liệu hoặc tên món.
- Xem chi tiết cách nấu, nguyên liệu cần thiết.
- Lưu món yêu thích để dùng lại.
- Tối ưu việc nấu nướng, tiết kiệm thời gian nghĩ “hôm nay ăn gì?”.

## 🚀 Đối tượng sử dụng

- Người bận rộn muốn chuẩn bị bữa ăn nhanh gọn.
- Người muốn ăn theo chế độ dinh dưỡng (eat clean, keto…).
- Người sống một mình hoặc nhóm nhỏ.

---

## 🛠 Tính năng cần thiết (MVP)

### 1. Authentication

- Đăng ký / Đăng nhập bằng email + mật khẩu.
- Lưu token (JWT) để xác thực các request GraphQL.

### 2. Recipe Management

- Tìm kiếm món ăn theo tên hoặc nguyên liệu.
- Xem chi tiết món ăn:
  - Nguyên liệu.
  - Cách làm.
  - Thời gian nấu.
- Lưu món yêu thích (favorites).

### 3. Meal Plan

- Tạo thực đơn cho từng ngày.
- Thêm / Xóa món ăn vào kế hoạch.
- Xem kế hoạch ăn uống theo lịch.

---

## 📦 Công nghệ

- **Monorepo**: Nx hoặc Turborepo.
- **Frontend**: Next.js + Apollo Client + Tailwind CSS.
- **Backend**: NestJS + GraphQL + Apollo Server.
- **Database**: PostgreSQL (Supabase/Railway).
- **Triển khai**:
  - FE: Vercel
  - BE: Railway/Render
  - DB: Supabase

---

## 🗓 Lộ trình phát triển MVP (2 tuần)

- **Tuần 1**:
  - Setup monorepo.
  - Backend: Auth + Recipe + Ingredient module.
  - Frontend: Auth page + Recipe list + Search.
- **Tuần 2**:
  - Backend: MealPlan + Favorites.
  - Frontend: Meal plan UI + Recipe detail + Favorites page.
  - Deploy & test bản đầu.

---

## 📈 Hướng mở rộng

- AI gợi ý thực đơn theo nguyên liệu còn lại.
- Chế độ ăn theo mục tiêu dinh dưỡng.
- Chia sẻ món ăn trong cộng đồng.
- Gợi ý mua nguyên liệu từ siêu thị online.
