# نظام إدارة أداء التسويق 📊

نظام متكامل لإدارة وتتبع أداء المسوقين على منصات TikTok و Instagram، مبني باستخدام HTML/JS خالص مع Supabase كقاعدة بيانات سحابية.

---

## 🚀 الرفع على Vercel

### الطريقة الأولى: عبر GitHub (مُوصى بها)

1. **ارفع المشروع على GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

2. **اربط GitHub بـ Vercel:**
   - افتح [vercel.com](https://vercel.com) وسجل الدخول
   - اضغط **"Add New Project"**
   - اختر الـ Repository من GitHub
   - اضغط **"Deploy"** — سيكتشف Vercel الإعدادات تلقائياً

3. **بعد النشر:** ستحصل على رابط مثل `https://your-project.vercel.app`

### الطريقة الثانية: رفع مباشر بدون GitHub
```bash
npm i -g vercel
vercel --prod
```

---

## 🗄️ إعداد Supabase

البيانات مربوطة مسبقاً. تأكد من إنشاء الجداول التالية في Supabase:

### الجداول المطلوبة

#### جدول `marketers`
```sql
CREATE TABLE marketers (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  "targetTikTok" INTEGER DEFAULT 15,
  "targetInstagram" INTEGER DEFAULT 15,
  "isActive" BOOLEAN DEFAULT true,
  "createdDate" TIMESTAMPTZ DEFAULT NOW()
);
```

#### جدول `accounts`
```sql
CREATE TABLE accounts (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  platform TEXT NOT NULL,
  "marketerId" INTEGER REFERENCES marketers(id),
  "isActive" BOOLEAN DEFAULT true
);
```

#### جدول `daily_reports`
```sql
CREATE TABLE daily_reports (
  id SERIAL PRIMARY KEY,
  "marketerId" INTEGER REFERENCES marketers(id),
  "accountId" INTEGER REFERENCES accounts(id),
  "reportDate" DATE NOT NULL,
  "morningTikTok" INTEGER DEFAULT 0,
  "scheduledTikTok" INTEGER DEFAULT 0,
  "morningInstagram" INTEGER DEFAULT 0,
  "scheduledInstagram" INTEGER DEFAULT 0,
  "imageDesigns" INTEGER DEFAULT 0,
  "aiVideos" INTEGER DEFAULT 0,
  notes TEXT,
  "createdAt" TIMESTAMPTZ DEFAULT NOW()
);
```

### تفعيل Row Level Security (RLS)
```sql
-- تفعيل RLS على الجداول
ALTER TABLE marketers ENABLE ROW LEVEL SECURITY;
ALTER TABLE accounts ENABLE ROW LEVEL SECURITY;
ALTER TABLE daily_reports ENABLE ROW LEVEL SECURITY;

-- السماح للمستخدمين المسجلين بالقراءة والكتابة
CREATE POLICY "authenticated users full access" ON marketers
  FOR ALL USING (auth.role() = 'authenticated');

CREATE POLICY "authenticated users full access" ON accounts
  FOR ALL USING (auth.role() = 'authenticated');

CREATE POLICY "authenticated users full access" ON daily_reports
  FOR ALL USING (auth.role() = 'authenticated');
```

---

## 🔐 بيانات الاتصال

```
SUPABASE_URL: https://gbqynlsuwkrnwopwfnwl.supabase.co
SUPABASE_ANON_KEY: (موجودة في index.html)
```

---

## 📦 هيكل المشروع

```
/
├── index.html      ← التطبيق الكامل (HTML + CSS + JS)
├── vercel.json     ← إعدادات Vercel للنشر
└── README.md       ← هذا الملف
```

---

## ✨ الميزات

- 🔐 تسجيل دخول/خروج عبر Supabase Auth
- 👥 إدارة المسوقين (إضافة/تعديل/حذف)
- 📱 إدارة الحسابات (TikTok & Instagram)
- 📝 تقارير يومية للأداء
- 📊 لوحة تحكم تفاعلية
- 🏆 ترتيب الأداء (Leaderboard)
- 📅 تقارير شهرية
- 🌙 واجهة عربية RTL داكنة
