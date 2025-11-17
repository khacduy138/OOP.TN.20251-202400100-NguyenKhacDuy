# Tại sao những đường dẫn `.settings`, `bin`, `.classpath`, `.project` nên được thêm vào `.gitignore`? Nếu không thêm thì sao?

Những tệp và thư mục này (`.settings/`, `bin/`, `.classpath`, `.project`) là các tệp cấu hình và kết quả biên dịch do môi trường phát triển Eclipse tự động tạo ra. Chúng nên được thêm vào `.gitignore` vì:

## **1. Cấu hình dành riêng cho môi trường local**
Các tệp này chứa các cài đặt dành riêng cho máy tính của một lập trình viên (JDK path, thiết lập build...). Các cấu hình này có thể không phù hợp với máy của thành viên khác trong nhóm.

## **2. Có thể tạo ra conflicts không cần thiết**
Nếu commit các file này lên repository, mỗi khi IDE ghi lại cài đặt, Git sẽ nhận thấy thay đổi và dẫn đến **merge conflict vô nghĩa** giữa các lập trình viên.

## **3. Làm nặng repo**
`bin/` chứa các file `.class` — đây là **output**, không phải source code. Các file này làm repo nặng và rối.

**Nếu không ignore**, repo sẽ đầy file tạm, file cấu hình IDE dẫn đến gây rối, xung đột và khó hợp tác khi mỗi người dùng cài đặt IDE khác nhau.

---

# Nếu sử dụng IntelliJ IDEA hoặc VSCode, cần ignore gì?

## **IntelliJ IDEA**
Thêm vào `.gitignore`:
```
.idea/
*.iml
```

## **VSCode**
Thêm vào `.gitignore`:
```
.vscode/
```

---

# Làm thế nào để Git ngừng theo dõi file đã commit nhưng không xóa file khỏi máy?

Thêm tên file vào `.gitignore` không có tác dụng nếu file đó đã được Git theo dõi từ trước.  
Cần làm như sau:

## **Xóa file/folder khỏi index nhưng giữ lại file/folder trên máy và commit thay đổi**
```
git rm --cached <file_name>
git commit -m "Stop tracking IDE configuration files"
```

Khi đó, Git sẽ ngừng theo dõi file đó và các thay đổi sau này sẽ được ignore như mong muốn.
