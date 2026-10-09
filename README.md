# Đóng gói APK cho ứng dụng học từ vựng

Ứng dụng chạy hoàn toàn offline (không cần máy chủ, không cần Claude). Thư mục `www/` là toàn bộ app.

## Cách A: build APK miễn phí bằng GitHub (không cần cài Android Studio)
1. Tạo tài khoản GitHub, tạo repository mới (để Private cũng được).
2. Tải toàn bộ nội dung thư mục này lên repository (nhớ cả thư mục `.github`).
   Nếu giao diện web không tải được thư mục `.github`: chọn Add file → Create new file,
   gõ tên `.github/workflows/build-apk.yml` rồi dán nội dung file cùng tên vào.
3. Vào tab Actions → "Build APK" → Run workflow. Đợi khoảng 5–10 phút.
4. Mở lần chạy đã xong, kéo xuống mục Artifacts, tải `tu-vung-apk` (file zip chứa `app-debug.apk`).
5. Chép APK vào điện thoại Android, mở lên và cho phép "Cài đặt ứng dụng không rõ nguồn gốc".

## Cách B: build trên máy có Android Studio
```
npm install
npx cap add android
npx cap sync android
npx cap open android      # rồi Build > Build APK(s) trong Android Studio
```

## Định dạng file nhập
- `.json`: file tạo bởi nút Xuất của app.
- `.csv` hoặc `.tsv`: dòng đầu là tiêu đề. Cột bắt buộc: `word`, `meaning` (hoặc `vi`).
  Cột tuỳ chọn: `ipa`, `pos`, `example`, `topic`. Không có cột `topic` thì tên file làm tên chủ đề.
  Ví dụ:
  ```
  word,ipa,pos,meaning,example,topic
  airport,/ˈɛrpɔːrt/,n,sân bay,We arrived at the airport.,Du lịch
  ```
- Lưu CSV dạng UTF-8 để không lỗi dấu tiếng Việt.

## Ghi chú
- APK này là bản debug, đủ để tự cài. Muốn đưa lên Google Play cần build bản release có ký số.
- Dữ liệu lưu trong app trên điện thoại; hãy dùng Xuất file để sao lưu trước khi gỡ app.
