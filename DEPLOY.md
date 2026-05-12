# 🚀 Hướng dẫn deploy foo'die lên Vercel

## Bước 1: Tạo tài khoản Vercel
Vào https://vercel.com → Sign up bằng Google (miễn phí)

## Bước 2: Upload files lên GitHub
1. Vào https://github.com → New repository → đặt tên `foodie-app`
2. Upload 2 files: `index.html` và `manifest.json`

## Bước 3: Deploy lên Vercel
1. Vào Vercel → Add New Project
2. Import repo GitHub vừa tạo
3. Bấm Deploy → chờ ~1 phút
4. Vercel sẽ cho bạn link kiểu: `foodie-app.vercel.app`

## Bước 4: Fix Firebase Storage CORS (quan trọng!)
Nếu upload ảnh bị lỗi, cần chạy lệnh này 1 lần:

1. Cài Google Cloud SDK: https://cloud.google.com/sdk/docs/install
2. Tạo file `cors.json`:
```json
[
  {
    "origin": ["*"],
    "method": ["GET", "POST", "PUT"],
    "maxAgeSeconds": 3600
  }
]
```
3. Chạy: `gsutil cors set cors.json gs://foo-die-47235.firebasestorage.app`

## Bước 5: Cài lên iPhone (iOS)
1. Gửi link cho người yêu
2. Mở link bằng **Safari** (không dùng Chrome)
3. Bấm nút **Share** (ô vuông có mũi tên lên)
4. Chọn **"Add to Home Screen"**
5. Bấm **Add** → Icon xuất hiện trên màn hình!

## Firebase Rules (tuỳ chọn - bảo mật hơn)
Vào Firebase Console → Firestore → Rules, thay bằng:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /meals/{meal} {
      allow read, write: if true;
    }
  }
}
```

## Lưu ý
- App cần internet để hoạt động
- Ảnh upload lên Firebase Storage, miễn phí tới 5GB
- Spark plan (miễn phí) của Firebase đủ dùng cho 2 người
