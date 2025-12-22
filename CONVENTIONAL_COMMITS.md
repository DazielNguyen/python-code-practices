# Conventional Commits Setup

Repo này đã được cài đặt Commitizen để sử dụng conventional commits.

## Cách sử dụng

### Tạo commit với Commitizen (Khuyến nghị)
Thay vì `git commit -m "message"`, sử dụng:
```bash
cz commit
```
hoặc
```bash
cz c
```

Commitizen sẽ hướng dẫn bạn qua các bước:
1. Chọn loại commit (feat, fix, docs, style, refactor, test, chore, etc.)
2. Nhập scope (optional)
3. Nhập mô tả ngắn
4. Nhập mô tả chi tiết (optional)
5. Breaking changes (optional)
6. Issues liên quan (optional)

### Các loại commit phổ biến:
- `feat`: Thêm tính năng mới
- `fix`: Sửa bug
- `docs`: Thay đổi documentation
- `style`: Thay đổi code style (không ảnh hưởng logic)
- `refactor`: Refactor code
- `test`: Thêm hoặc sửa tests
- `chore`: Công việc bảo trì (dependencies, config, etc.)
- `perf`: Cải thiện performance
- `ci`: Thay đổi CI configuration

### Ví dụ commit messages:
```
feat: add solution for problem 242 valid anagram
fix: correct time complexity in 217 solution
docs: update README with new problem structure
chore: setup commitizen for conventional commits
```

### Bump version và tạo changelog
```bash
cz bump
```

### Xem changelog
```bash
cz changelog
```

## Pre-commit Hook (Tùy chọn)
Để tự động validate commit messages, cài đặt pre-commit hook:
```bash
pip install pre-commit
pre-commit install --hook-type commit-msg
```
