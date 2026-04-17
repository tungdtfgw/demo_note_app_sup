---
description: 'Workflow đầy đủ để implement một feature: plan → verify → code → test → fix'
agent: 'agent'
tools: ['terminal', 'search/codebase', 'read', 'edit']
argument-hint: 'tên hoặc mô tả feature cần implement'
---
# Implement Feature

Workflow đầy đủ để implement một feature cho MyNotes. **Không bỏ qua bước nào.**

## Bước 1: Đọc context

Đọc các file sau theo thứ tự để hiểu feature cần làm:

1. [PRD.md](../../PRD.md) — yêu cầu sản phẩm, tính năng đã chốt
2. [SCREENS.md](../../SCREENS.md) — flow thao tác người dùng, happy paths và edge cases
3. [DB.md](../../DB.md) — schema, RLS, indexes, queries liên quan
4. [AGENTS.md](../../AGENTS.md) — trạng thái hiện tại, những gì đã làm, TODOs
5. [mistakes.md](../../mistakes.md) — các lỗi đã gặp để tránh lặp lại

Xác định feature cần implement: `${input:feature:tên hoặc mô tả feature}`

## Bước 2: Tạo plan

Tạo file `plan-${input:feature}.md` trong thư mục gốc với nội dung:

```markdown
# Plan: [tên feature]

## Mục tiêu
[1-2 câu mô tả feature cần làm]

## Các file cần tạo / sửa
- [ ] `path/to/file.tsx` — mô tả ngắn
- [ ] `path/to/file.ts` — mô tả ngắn

## Migration (nếu cần thay đổi DB)
- [ ] SQL migration cần tạo

## Các bước implement
1. [bước 1]
2. [bước 2]
3. ...

## Test cases
- [ ] [test case 1]
- [ ] [test case 2]

## Edge cases từ SCREENS.md
- [ ] [edge case 1]
- [ ] [edge case 2]
```

**Hiển thị plan và DỪNG LẠI. Chờ người dùng xác nhận trước khi code.**

## Bước 3: Implement

Sau khi người dùng xác nhận plan:

1. **Migration** (nếu có): Tạo file SQL trong `supabase/migrations/`. Sử dụng **Supabase Skill** để viết SQL đúng chuẩn (indexes, RLS, constraints).
2. **Services**: Tạo/sửa các hàm trong `src/services/`. Sử dụng **Supabase Skill** cho queries tối ưu. Dùng **Context7 MCP** nếu cần tra cứu API Supabase client.
3. **Hooks**: Tạo/sửa custom hooks trong `src/hooks/`.
4. **Components**: Tạo/sửa UI components. Sử dụng **Expo Skill** cho patterns React Native, navigation, styling.
5. **Screens**: Kết nối components vào màn hình. Tham khảo SCREENS.md cho flow và edge cases.

Tuân thủ mọi quy tắc trong `copilot-instructions.md` và `react-native.instructions.md`.

## Bước 4: Viết unit test

Sử dụng **React Native Testing Toolkit** skill để viết test:

1. Tạo file test cạnh file source: `[name].test.tsx` hoặc `[name].test.ts`.
2. Cover các test cases đã liệt kê trong plan.
3. Cover các edge cases từ SCREENS.md.
4. Mock Supabase client — không gọi API thật trong test.

## Bước 5: Chạy test và sửa lỗi

1. Chạy `npm test -- --watchAll=false` để chạy toàn bộ test.
2. Nếu có test FAIL:
   - Đọc error message và xác định nguyên nhân.
   - Sửa code (không sửa test trừ khi test sai).
   - Chạy lại test.
   - Lặp lại cho đến khi tất cả PASS.
3. Nếu tất cả PASS: báo cáo kết quả.

## Bước 6: Tổng kết

Báo cáo cho người dùng:
- Các file đã tạo / sửa
- Kết quả test (bao nhiêu test, tất cả pass)
- Gợi ý chạy `/wrap-up` để cập nhật AGENTS.md
- Gợi ý chạy `/git-commit` để commit thay đổi
