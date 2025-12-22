# 242. Valid Anagram

## Đề bài

Cho hai chuỗi `s` và `t`, trả về `True` nếu `t` là một anagram của `s`, và `False` nếu không phải.

**Anagram** là một từ hoặc cụm từ được tạo thành bằng cách sắp xếp lại các chữ cái của một từ khác, sử dụng tất cả các chữ cái gốc đúng một lần.

**Ví dụ:**
- Input: s = "anagram", t = "nagaram" → Output: True
- Input: s = "rat", t = "car" → Output: False

---

## 1. Các cách giải với độ phức tạp O(n²)

### 1.1. Brute Force - Count từng ký tự

**Ý tưởng:** Với mỗi ký tự trong chuỗi `s`, đếm số lần xuất hiện của nó trong cả `s` và `t`.

**Cách hoạt động:**

1. Kiểm tra độ dài của 2 chuỗi, nếu khác nhau thì không thể là anagram → trả về `False`
2. Duyệt qua từng ký tự trong `s`
3. Đếm số lần xuất hiện của ký tự đó trong `s` và `t`
4. Nếu số lần xuất hiện khác nhau → trả về `False`
5. Nếu tất cả ký tự đều có cùng số lần xuất hiện → trả về `True`

**Độ phức tạp:**

- Thời gian: O(n²) - với mỗi ký tự trong `s` (n lần), phải đếm trong cả 2 chuỗi (n lần)
- Không gian: O(1) - không dùng thêm bộ nhớ phụ

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        for char in s:
            if s.count(char) != t.count(char):
                return False
        return True
```

---

## 2. Các cách giải với độ phức tạp O(n log n)

### 2.1. Sorting

**Ý tưởng:** Nếu 2 chuỗi là anagram của nhau, sau khi sắp xếp chúng sẽ giống hệt nhau.

**Cách hoạt động:**

1. Kiểm tra độ dài của 2 chuỗi, nếu khác nhau thì không thể là anagram → trả về `False`
2. Sắp xếp cả 2 chuỗi theo thứ tự alphabet
3. So sánh 2 chuỗi đã sắp xếp
   - Nếu giống nhau → trả về `True`
   - Nếu khác nhau → trả về `False`

**Độ phức tạp:**

- Thời gian: O(n log n) - do thuật toán sắp xếp (Timsort trong Python)
- Không gian: O(n) - tạo ra 2 chuỗi mới đã sắp xếp

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        return sorted(s) == sorted(t)
```

**Cách viết gọn hơn:**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```

---

## 3. Các cách giải với độ phức tạp O(n)

### 3.1. Hash Map (Dictionary)

**Ý tưởng:** Đếm tần suất xuất hiện của mỗi ký tự trong cả 2 chuỗi, sau đó so sánh.

**Cách 1: Sử dụng 2 Hash Map**

**Cách hoạt động:**

1. Kiểm tra độ dài của 2 chuỗi, nếu khác nhau → trả về `False`
2. Tạo 2 Dictionary để đếm tần suất ký tự cho từng chuỗi
3. Duyệt qua chuỗi `s` và đếm tần suất mỗi ký tự
4. Duyệt qua chuỗi `t` và đếm tần suất mỗi ký tự
5. So sánh 2 Dictionary
   - Nếu giống nhau → trả về `True`
   - Nếu khác nhau → trả về `False`

**Độ phức tạp:**

- Thời gian: O(n) - duyệt qua mỗi chuỗi 1 lần
- Không gian: O(n) - lưu trữ tần suất của các ký tự

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        count_s = {}
        count_t = {}
        
        for char in s:
            count_s[char] = count_s.get(char, 0) + 1
        
        for char in t:
            count_t[char] = count_t.get(char, 0) + 1
        
        return count_s == count_t
```

**Cách 2: Sử dụng 1 Hash Map**

**Cách hoạt động:**

1. Kiểm tra độ dài của 2 chuỗi, nếu khác nhau → trả về `False`
2. Tạo 1 Dictionary để theo dõi sự chênh lệch tần suất
3. Duyệt qua chuỗi `s`, tăng count cho mỗi ký tự
4. Duyệt qua chuỗi `t`, giảm count cho mỗi ký tự
5. Kiểm tra tất cả giá trị trong Dictionary
   - Nếu tất cả đều bằng 0 → trả về `True`
   - Nếu có giá trị khác 0 → trả về `False`

**Độ phức tạp:**

- Thời gian: O(n) - duyệt qua mỗi chuỗi 1 lần
- Không gian: O(n) - lưu trữ tần suất của các ký tự

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        char_count = {}
        
        for char in s:
            char_count[char] = char_count.get(char, 0) + 1
        
        for char in t:
            char_count[char] = char_count.get(char, 0) - 1
        
        for count in char_count.values():
            if count != 0:
                return False
        
        return True
```

**Cách 3: Tối ưu với early return**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        char_count = {}
        
        for char in s:
            char_count[char] = char_count.get(char, 0) + 1
        
        for char in t:
            if char not in char_count:
                return False
            char_count[char] -= 1
            if char_count[char] < 0:
                return False
        
        return True
```

---

### 3.2. Counter (từ thư viện collections)

**Ý tưởng:** Sử dụng `Counter` của Python để đếm tần suất ký tự tự động.

**Cách hoạt động:**

1. Sử dụng `Counter` để đếm tần suất ký tự trong cả 2 chuỗi
2. So sánh 2 `Counter` objects
   - Nếu giống nhau → trả về `True`
   - Nếu khác nhau → trả về `False`

**Độ phức tạp:**

- Thời gian: O(n) - `Counter` duyệt qua chuỗi 1 lần
- Không gian: O(n) - lưu trữ tần suất của các ký tự

```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```

---

### 3.3. Array/List với 26 ký tự (chỉ dành cho chữ cái thường)

**Ý tưởng:** Nếu đề bài giới hạn chỉ có chữ cái thường (a-z), có thể dùng mảng có độ dài cố định 26.

**Cách hoạt động:**

1. Tạo mảng có 26 phần tử (tương ứng với 26 chữ cái) khởi tạo bằng 0
2. Duyệt qua chuỗi `s`, tăng count tại vị trí tương ứng
3. Duyệt qua chuỗi `t`, giảm count tại vị trí tương ứng
4. Kiểm tra nếu tất cả phần tử trong mảng đều bằng 0 → trả về `True`, ngược lại `False`

**Độ phức tạp:**

- Thời gian: O(n) - duyệt qua mỗi chuỗi 1 lần
- Không gian: O(1) - mảng có kích thước cố định 26

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        # Mảng đếm cho 26 chữ cái a-z
        char_count = [0] * 26
        
        for i in range(len(s)):
            # Tăng count cho ký tự trong s
            char_count[ord(s[i]) - ord('a')] += 1
            # Giảm count cho ký tự trong t
            char_count[ord(t[i]) - ord('a')] -= 1
        
        # Kiểm tra nếu tất cả đều bằng 0
        for count in char_count:
            if count != 0:
                return False
        
        return True
```

**Cách viết ngắn gọn hơn:**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        char_count = [0] * 26
        
        for i in range(len(s)):
            char_count[ord(s[i]) - ord('a')] += 1
            char_count[ord(t[i]) - ord('a')] -= 1
        
        return all(count == 0 for count in char_count)
```

---

## Tổng kết

### So sánh các phương pháp:

| Phương pháp | Thời gian | Không gian | Ưu điểm | Nhược điểm |
|-------------|-----------|------------|---------|------------|
| Brute Force | O(n²) | O(1) | Đơn giản, không cần thêm bộ nhớ | Chậm với chuỗi dài |
| Sorting | O(n log n) | O(n) | Code ngắn gọn, dễ hiểu | Chậm hơn O(n) |
| Hash Map (2 dict) | O(n) | O(n) | Nhanh, rõ ràng | Tốn bộ nhớ |
| Hash Map (1 dict) | O(n) | O(n) | Nhanh, tiết kiệm bộ nhớ hơn | Code phức tạp hơn |
| Counter | O(n) | O(n) | Code ngắn nhất, dễ đọc | Cần import thư viện |
| Array 26 | O(n) | O(1) | Nhanh nhất, không gian cố định | Chỉ dùng cho chữ cái thường |

### Lựa chọn phương pháp:

- **Interview/Production**: Hash Map hoặc Counter (O(n))
- **Code ngắn gọn**: `Counter(s) == Counter(t)` hoặc `sorted(s) == sorted(t)`
- **Tối ưu nhất**: Array 26 phần tử (nếu chỉ có chữ cái thường)
- **Học thuật**: Nên hiểu và thực hành cả 3 cách: Sorting, Hash Map, và Array

---

## Follow-up Questions

**Q: Nếu input chứa ký tự Unicode thì sao?**
- **A:** Sử dụng Hash Map/Counter thay vì Array 26 phần tử vì số lượng ký tự Unicode rất lớn.

**Q: Cách nào tốt nhất?**
- **A:** 
  - Nếu chỉ có chữ cái thường: Array 26 phần tử (O(n) thời gian, O(1) không gian)
  - Nếu có nhiều loại ký tự: Counter (code ngắn) hoặc Hash Map (hiệu suất tốt)
  - Nếu cần code ngắn gọn nhất: `sorted(s) == sorted(t)`
