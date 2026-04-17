---
name: 'Quy tắc React Native'
description: 'Quy tắc code riêng của dự án MyNotes cho các file TypeScript và React Native'
applyTo: 'src/**/*.tsx,src/**/*.ts'

---

# Quy tắc React Native — MyNotes

## Expo Skills

Luôn sử dụng Expo Skills khi code. Expo Skills đã cover các pattern chung về expo-router, FlatList, Platform API, và các Expo module. File này chỉ chứa quy tắc **riêng của dự án MyNotes** — không lặp lại những gì Expo Skills đã có.

## Components

- Chỉ dùng functional components. Không dùng class components.
- Export dạng named export, mỗi file một component.
- Giữ component dưới 150 dòng. Tách logic vào custom hooks.
- Chỉ dùng `React.memo` khi đo được vấn đề hiệu năng thực tế — không dùng mặc định.

## Styling

- Dùng `StyleSheet.create` ở cuối mỗi file component.
- Không dùng inline style objects, không dùng CSS-in-JS.
- Nhóm styles theo logic: `container`, `header`, `content`, `footer`.
- Dùng giá trị spacing nhất quán: 4, 8, 12, 16, 24, 32.

## Quản lý state

- **State cục bộ:** `useState` cho state chỉ dùng trong UI (modal, input, toggle).
- **State toàn cục:** React Context + `useReducer` cho state dùng chung (danh sách ghi chú, cài đặt).
- Không gọi Supabase bên trong reducer. Dispatch action trước, persist trong hook/effect sau.

## Tầng Services (Supabase)

- Mọi truy cập Supabase đặt trong `src/services/`. Components không import `@supabase/supabase-js` trực tiếp.
- Các hàm service phải async, trả về kết quả có kiểu rõ ràng, và tự xử lý lỗi.
- Đặt tên hàm rõ nghĩa: `getNoteById`, `saveNote`, `softDeleteNote`, `searchNotes`, `getCategories`.

## Accessibility

- Thêm `accessibilityLabel` cho mọi phần tử chạm được và icon.
- Dùng `accessibilityRole` (button, header, link) khi phù hợp.
- Vùng chạm tối thiểu 44x44 points.

## TypeScript

- Đặt types dùng chung trong `src/types/`. Types riêng của component đặt cùng file component.
- Dùng `interface` cho object shapes, `type` cho unions và intersections.
- Không dùng `any`. Dùng `unknown` + type guards khi kiểu thực sự không chắc chắn.
