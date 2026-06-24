# Marketing Performance Management System

## نظام إدارة أداء التسويق

### طريقة الرفع على Vercel:

#### الطريقة 1: Vercel Drop (الأسهل)
1. افتح: https://vercel.com/drop
2. اسحب هذا المجلد بأكمله وأفلته في الصفحة
3. اضغط Deploy
4. خلال 30 ثانية، الموقع جاهز!

#### الطريقة 2: GitHub + Vercel
1. ارفع هذا المجلد على GitHub
2. اربط GitHub بـ Vercel
3. اضغط Deploy

### ⚠️ تعديلات مهمة قبل الاستخدام:

#### 1. إنشاء حساب Supabase:
- ادخل إلى: https://supabase.com
- سجل حساب جديد (مجاني)
- أنشئ مشروع جديد
- اذهب إلى Project Settings → API
- انسخ: Project URL و anon public key

#### 2. إنشاء الجداول في Supabase:

**جدول marketers:**
- id (int8, Primary Key, Auto Increment)
- name (text)
- targetTikTok (int4, Default: 15)
- targetInstagram (int4, Default: 15)
- isActive (bool, Default: true)
- createdDate (timestamptz, Default: now())

**جدول accounts:**
- id (int8, Primary Key, Auto Increment)
- name (text)
- platform (text)
- marketerId (int8)
- isActive (bool, Default: true)

**جدول daily_reports:**
- id (int8, Primary Key, Auto Increment)
- reportDate (date)
- marketerId (int8)
- accountId (int8)
- morningTikTok (int4, Default: 0)
- morningInstagram (int4, Default: 0)
- scheduledTikTok (int4, Default: 0)
- scheduledInstagram (int4, Default: 0)
- imageDesigns (int4, Default: 0)
- aiVideos (int4, Default: 0)
- notes (text)

#### 3. تفعيل Auth:
- اذهب إلى Authentication → Providers
- فعّل Email
- اذهب إلى URL Configuration
- أضف: Site URL = رابط Vercel الخاص بك

#### 4. تعديل الكود:
افتح index.html وابحث عن:
```javascript
const SUPABASE_URL = 'https://your-project.supabase.co';
const SUPABASE_ANON_KEY = 'your-anon-key';
```
واستبدلهم بقيمك من Supabase.

### البيانات المدمجة:
- 16 مسوق من ملف Excel
- 18 حساب (36 مع المنصات)
- مرتبطين بـ MarketerID

### المميزات:
- ✅ تصميم أسود وذهبي
- ✅ تسجيل دخول Supabase Auth
- ✅ قاعدة بيانات سحابية
- ✅ Dashboard مع KPIs
- ✅ إدارة المسوقين والحسابات
- ✅ تقارير يومية وشهرية
- ✅ Leaderboard
- ✅ حسابات تلقائية (Total, Performance%)
