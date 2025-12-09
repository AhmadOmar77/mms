# CareNow - Quick Start Guide

## 🚀 دليل البدء السريع (Quick Start)

### المتطلبات الأساسية (Prerequisites)

قبل البدء، تأكد من تثبيت:

- **PHP 8.1+** مع SQLite extension
- **Composer** (PHP dependency manager)
- **Node.js 18+** و npm
- **Git** (اختياري)

---

## خطوات التشغيل (Setup Steps)

### 1️⃣ استخراج المشروع (Extract Project)

```bash
# فك ضغط الملف
tar -xzf carenow-complete-project.tar.gz

# الدخول إلى المجلد
cd carenow-fullstack
```

### 2️⃣ إعداد Backend (Laravel)

```bash
# تثبيت اعتماديات PHP
composer install

# نسخ ملف البيئة
cp .env.example .env

# توليد مفتاح التطبيق
php artisan key:generate

# إنشاء قاعدة البيانات
touch database/database.sqlite

# تشغيل migrations
php artisan migrate

# تشغيل الخادم
php artisan serve
```

✅ **Backend جاهز على**: `http://localhost:8000`

### 3️⃣ إعداد Frontend (React)

افتح نافذة terminal جديدة:

```bash
# في نفس المجلد carenow-fullstack

# تثبيت اعتماديات Node
npm install

# تشغيل خادم التطوير
npm run dev
```

✅ **Frontend جاهز على**: `http://localhost:5173`

---

## 🧪 اختبار النظام (Testing)

### 1. التسجيل (Registration)
1. افتح المتصفح على `http://localhost:5173`
2. اضغط على "Create Profile" أو انتقل إلى `/register`
3. املأ البيانات:
   - **Name**: اسمك الكامل
   - **Email**: بريدك الإلكتروني
   - **Phone**: رقم هاتفك
   - **Role**: اختر "Patient"
   - **Password**: كلمة مرور قوية
4. اضغط "Create Account"

### 2. تسجيل الدخول (Login)
- سيتم تسجيل دخولك تلقائيًا بعد التسجيل
- أو اذهب إلى `/login` واستخدم بياناتك

### 3. لوحة التحكم (Dashboard)
- ستظهر لك لوحة التحكم الرئيسية
- يمكنك رؤية:
  - زر الطوارئ الأحمر
  - بطاقات الوصول السريع
  - معلومات حسابك

### 4. اختبار زر الطوارئ (Emergency Button)
1. اضغط على زر "Emergency Alert"
2. السماح للمتصفح بالوصول إلى موقعك
3. سيتم إرسال تنبيه طوارئ مع موقعك

### 5. الملف الطبي (Medical Profile)
1. اضغط على "Medical Profile" من Dashboard
2. املأ معلوماتك الطبية:
   - فصيلة الدم
   - تاريخ الميلاد
   - الجنس
   - معلومات الاتصال في حالات الطوارئ
3. احفظ البيانات

---

## 🔑 حسابات تجريبية (Test Accounts)

يمكنك إنشاء حسابات تجريبية بأدوار مختلفة:

### مريض (Patient)
```
Email: patient@test.com
Password: password123
Role: Patient
```

### طبيب (Doctor)
```
Email: doctor@test.com
Password: password123
Role: Doctor
```

### سائق إسعاف (Ambulance Driver)
```
Email: driver@test.com
Password: password123
Role: Ambulance Driver
```

---

## 📱 API Testing

يمكنك اختبار API مباشرة باستخدام cURL أو Postman:

### تسجيل مستخدم جديد
```bash
curl -X POST http://localhost:8000/api/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "password": "password123",
    "password_confirmation": "password123",
    "phone": "+1234567890",
    "role": "patient"
  }'
```

### تسجيل الدخول
```bash
curl -X POST http://localhost:8000/api/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123"
  }'
```

### إنشاء تنبيه طوارئ
```bash
curl -X POST http://localhost:8000/api/emergency-alerts \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN_HERE" \
  -d '{
    "latitude": 30.0444,
    "longitude": 31.2357,
    "address": "Cairo, Egypt"
  }'
```

---

## 🐛 حل المشاكل (Troubleshooting)

### مشكلة: "could not find driver"
```bash
# تثبيت SQLite extension
sudo apt-get install php8.1-sqlite3
# أو
sudo yum install php-sqlite3
```

### مشكلة: "Class not found"
```bash
# إعادة تحميل autoload
composer dump-autoload
```

### مشكلة: "CORS error"
```bash
# تأكد من تشغيل Backend على المنفذ 8000
# تأكد من تشغيل Frontend على المنفذ 5173
```

### مشكلة: "Migration failed"
```bash
# حذف قاعدة البيانات وإعادة إنشائها
rm database/database.sqlite
touch database/database.sqlite
php artisan migrate:fresh
```

### مشكلة: Frontend لا يعمل
```bash
# حذف node_modules وإعادة التثبيت
rm -rf node_modules
npm install
npm run dev
```

---

## 📂 الملفات المهمة (Important Files)

### Backend
- **Routes**: `routes/api.php`
- **Controllers**: `app/Http/Controllers/API/`
- **Models**: `app/Models/`
- **Migrations**: `database/migrations/`
- **Config**: `.env`

### Frontend
- **Pages**: `frontend-src/pages/`
- **Components**: `frontend-src/components/`
- **Routes**: `frontend-src/App.tsx`
- **Config**: `vite.config.ts`

### Documentation
- **ERD**: `docs/erd-diagram.png`
- **Use Cases**: `docs/use-case-diagram.png`
- **System Design**: `docs/SYSTEM_DESIGN.md`
- **README**: `CARENOW_README.md`

---

## 🎯 الخطوات التالية (Next Steps)

1. ✅ استكشف لوحة التحكم
2. ✅ أكمل ملفك الطبي
3. ✅ جرب زر الطوارئ
4. ✅ تصفح الأطباء (قريبًا)
5. ✅ احجز استشارة (قريبًا)

---

## 📞 الدعم (Support)

للمساعدة أو الأسئلة:
- راجع `CARENOW_README.md`
- راجع `docs/SYSTEM_DESIGN.md`
- راجع `PROJECT_DELIVERY.md`

---

## ✨ نصائح (Tips)

- استخدم **Chrome** أو **Firefox** للحصول على أفضل تجربة
- فعّل **Location Services** لاختبار زر الطوارئ
- افتح **Developer Console** (F12) لرؤية API requests
- استخدم **Postman** لاختبار API بشكل مفصل

---

**CareNow** - صحتك، أولويتنا 🏥

تم إنشاؤه بـ ❤️ باستخدام Laravel + React
