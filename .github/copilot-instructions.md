# Project: MyNotes

Ứng dụng ghi chú trên điện thoại, xây dựng bằng React Native + Expo, sử dụng Supabase làm backend. Người dùng đăng nhập bằng email magic link, dữ liệu lưu trên Supabase và đồng bộ qua nhiều thiết bị.

## Tech Stack

- **Runtime:** React Native với Expo SDK 54
- **Ngôn ngữ:** TypeScript (strict mode)
- **Routing:** expo-router (file-based)
- **Backend:** Supabase (Auth, Database, Row Level Security)
- **Auth:** Supabase Auth — email magic link, không dùng mật khẩu
- **Database:** Supabase PostgreSQL — truy vấn thông qua `@supabase/supabase-js`
- **Lưu trữ cục bộ:** AsyncStorage cho preferences và session
- **State:** React Context + useReducer (global), useState (local)

## Cấu trúc thư mục

```
src/
  screens/        — Các màn hình (mapped bởi expo-router)
  components/     — UI components tái sử dụng
  hooks/          — Custom React hooks
  utils/          — Hàm tiện ích thuần (pure functions)
  services/       — Tầng truy cập Supabase (CRUD, auth, queries)
  types/          — TypeScript types và interfaces dùng chung
  config/         — Cấu hình Supabase client, constants
```

## Quy ước đặt tên

- Components & types: `PascalCase` (`NoteCard.tsx`, `NoteType`)
- Hàm & biến: `camelCase` (`formatDate`, `noteCount`)
- File & thư mục: `kebab-case` (`note-card.tsx`, `use-notes.ts`)
- Hằng số: `UPPER_SNAKE_CASE` (`MAX_TITLE_LENGTH`)

## Quy tắc bắt buộc

- **Chỉ kết nối Supabase.** Không dùng fetch/axios trực tiếp tới bất kỳ API nào khác. Mọi truy cập dữ liệu đi qua Supabase client.
- **Không gọi Supabase trong components.** Mọi truy vấn và mutation đặt trong `src/services/`, components chỉ gọi qua hooks.
- **Không inline styles.** Dùng `StyleSheet.create` duy nhất.
- **Không lưu Supabase keys trong code.** Dùng biến môi trường (`EXPO_PUBLIC_SUPABASE_URL`, `EXPO_PUBLIC_SUPABASE_ANON_KEY`).
- **Ưu tiên package của Expo.** Chỉ thêm thư viện bên thứ ba khi Expo không có tương đương.
- **Code comments và commit messages viết bằng tiếng Anh.**

## Xử lý lỗi

- Bọc mọi thao tác Supabase trong try/catch.
- Kiểm tra `error` trong response của Supabase trước khi dùng `data`.
- Hiển thị thông báo thân thiện cho người dùng — không bao giờ hiển thị lỗi thô.
- Ghi log lỗi kèm thông tin ngữ cảnh để debug.
- Xử lý riêng các lỗi auth: session hết hạn → chuyển về màn hình đăng nhập.

## Skills (bắt buộc sử dụng)

Luôn sử dụng các skill sau cho các tác vụ tương ứng. Không code mà không tham khảo skill phù hợp.

| Skill | Khi nào dùng | Cài đặt |
|-------|-------------|---------|
| **Expo Skills** | Mọi code liên quan React Native, expo-router, UI, navigation, styling, data fetching | `npx skills add expo/skills` |
| **Supabase Skills** | Viết migration SQL, RLS policies, indexes, queries, Supabase client, connection management | `npx skills add supabase/agent-skills --skill supabase-postgres-best-practices` |
| **React Native Testing Toolkit** | Viết unit test, component test, screen test, mock setup | `npx skillfish add fontezbrooks/react-native-testing react-native-testing` |

## MCP Servers

Các MCP server được cấu hình trong dự án:

| MCP | Mục đích | Khi nào dùng |
|-----|---------|-------------|
| **Context7** | Tra cứu documentation mới nhất của các thư viện (Expo, Supabase, React Native, v.v.) | Khi cần kiểm tra API, cú pháp, hoặc breaking changes của bất kỳ thư viện nào |
| **Supabase MCP** | Tương tác trực tiếp với Supabase project: quản lý schema, chạy SQL, kiểm tra RLS, xem logs | Khi cần tạo/sửa bảng, test query, debug RLS, hoặc kiểm tra dữ liệu trên Supabase |

## Quy trình implement feature

Khi implement một feature mới, **luôn tuân theo workflow** sau (hoặc dùng prompt `/implement-feature`):

1. **Đọc context:** PRD.md → SCREENS.md → DB.md → AGENTS.md → mistakes.md
2. **Tạo plan:** Viết `plan-<feature-id>.md` mô tả các bước implement
3. **Chờ verify:** Người dùng xác nhận plan trước khi code
4. **Implement:** Code theo plan, sử dụng skill tương ứng
5. **Viết test:** Dùng React Native Testing Toolkit skill viết unit test
6. **Chạy test:** `npm test` — nếu fail thì sửa và chạy lại
7. **Wrap up:** Dùng `/wrap-up` để cập nhật AGENTS.md

## Tài liệu dự án

| File | Vai trò | Cập nhật |
|------|---------|---------|
| [PRD.md](../PRD.md) | Yêu cầu sản phẩm | Cố định |
| [SCREENS.md](../SCREENS.md) | Mô tả màn hình và flow | Cố định |
| [DB.md](../DB.md) | Thiết kế database | Khi schema thay đổi |
| [AGENTS.md](../AGENTS.md) | Trạng thái hiện tại, thay đổi gần đây, TODOs | Mỗi session (qua `/wrap-up`) |
| [mistakes.md](../mistakes.md) | Các lỗi đã gặp và cách tránh | Khi có lỗi (qua `/learn-from-mistake`) |
