Enterممتاز، نكمل الآن آخر وثيقتين أساسيتين قبل بدء بناء Flutter فعليًا.


---

05_Project_Architecture.md

معلومات الوثيقة

الحقل	القيمة

نوع المشروع	Flutter Android Offline App
المعمارية	Clean Architecture
إدارة الحالة	Riverpod
قاعدة البيانات	Drift (SQLite)
التنقل	GoRouter



---

1. فلسفة المعمارية

تم تصميم التطبيق ليكون:

قابل للتوسع.

سهل الصيانة.

مفصول الطبقات.

مستقل عن أي خدمات خارجية.



---

2. الطبقات الأساسية

UI Layer (Presentation)
        ↓
State Management (Riverpod)
        ↓
Domain Layer (Business Logic)
        ↓
Repository Layer
        ↓
Data Source (SQLite - Drift)


---

3. هيكل المشروع

lib/

├── app/

│   ├── app.dart

│   ├── router.dart

│   └── providers.dart

│
├── core/

│   ├── database/

│   ├── theme/

│   ├── utils/

│   ├── constants/

│   └── widgets/
│
├── features/

│   ├── auth/

│   ├── dashboard/

│   ├── patients/

│   ├── doctors/

│   ├── tests/

│   ├── reports/

│   ├── settings/

│   └── backup/
│
├── domain/

│   ├── entities/

│   ├── repositories/

│   └── usecases/

│
├── data/

│   ├── models/

│   ├── repositories_impl/

│   └── local/
│
└── main.dart


---

4. تقسيم المسؤوليات

UI Layer

عرض البيانات.

استقبال الإدخال.

التنقل.


Riverpod

إدارة الحالة.

تحديث الواجهة.


Domain

منطق الأعمال.

القواعد الأساسية.


Data

التعامل مع SQLite.

تحويل البيانات.



---

5. قواعد التطوير

لا يوجد استعلام مباشر من UI.

كل البيانات تمر عبر Repository.

كل Feature مستقل.

لا يوجد كود مكرر.

كل Service له مسؤولية واحدة.



---

6. التعامل مع البيانات

مثال:

UI → Provider → UseCase → Repository → Drift DB


---

7. قابلية التوسع

يمكن لاحقًا إضافة:

Firebase Sync (اختياري).

API Server.

Multi-device sync.

Web version.


بدون تغيير البنية الأساسية.


---

8. الأمان

تشفير كلمات المرور.

عدم تخزين بيانات حساسة بدون حماية.

عزل البيانات بين المستخدمين (إذا تم تفعيل multi-user).



---

9. الأداء

Lazy loading للبيانات.

Pagination.

Indexes في SQLite.

تقليل إعادة بناء الواجهات.



---

10. مبدأ Offline First

كل العمليات تعمل بدون إنترنت:

إدخال البيانات.

تعديل البيانات.

البحث.

التقارير.

الإحصائيات.



---

06_UI_UX_Design_System.md

معلومات الوثيقة

الحقل	القيمة

التصميم	Material 3
اللغة	العربية (RTL)
المنصة	Android



---

1. فلسفة التصميم

التصميم يعتمد على:

البساطة.

السرعة.

وضوح البيانات.

تقليل الضغط على المستخدم.

واجهة مخصصة للمختبرات الطبية.



---

2. الألوان

اللون الأساسي

Primary: Blue Medical Tone


الألوان المساعدة

Success: Green

Warning: Orange

Error: Red

Info: Blue Light



---

3. الخطوط

Arabic Font: Cairo / IBM Plex Sans Arabic

English Font: Roboto



---

4. الأزرار

Primary Button

لون ثابت.

حواف دائرية.

أيقونة اختيارية.


Secondary Button

حدود فقط.

بدون تعبئة.



---

5. البطاقات (Cards)

ظل خفيف.

زوايا 12px.

عرض بيانات مختصرة.



---

6. الجداول

قابلة للتمرير.

دعم RTL كامل.

صفوف متناوبة اللون.



---

7. الإدخالات (Inputs)

حقل واضح.

Label دائم.

Validation مباشر.

دعم البحث داخل الحقول.



---

8. التنقل

Bottom Navigation

Dashboard

Patients

Tests

Reports

Settings



---

9. الأيقونات

Material Icons

رموز طبية عند الحاجة



---

10. الوضع الليلي

مدعوم بالكامل.

ألوان داكنة مريحة للعين.



---

11. تجربة المستخدم

تقليل النقرات.

أزرار سريعة.

بحث دائم في الأعلى.

حفظ تلقائي للبيانات.



---

12. قواعد التصميم

كل شاشة لها هدف واحد.

لا يوجد ازدحام في الواجهة.

الأهم دائمًا في الأعلى.

دعم الهاتف والتابلت.



---

13. تحسينات خاصة بالمختبر

عرض النتائج بشكل جدول طبي واضح.

تمييز النتائج غير الطبيعية بالألوان.

طباعة جاهزة بدون تعديل.

QR للتقارير.



---

الآن وصلنا لمرحلة مهمة جدًا

لقد أكملنا كل الوثائق الأساسية:

✔ تحليل المشروع
✔ قائمة الميزات
✔ تحليل الشاشات
✔ تصميم قاعدة البيانات
✔ معمارية المشروع
✔ نظام التصميم


---

المرحلة التالية (الأهم)

الآن ننتقل إلى التنفيذ الفعلي:

01_Create Flutter Project

02_Setup Drift SQLite

03_Create Database Tables

04_Build First Feature (Patients Module)


---

إذا قلت "ابدأ التنفيذ" سأبدأ مباشرة في:

إنشاء مشروع Flutter.

إعداد الهيكل الكامل.

إعداد قاعدة البيانات.

بناء أول شاشة حقيقية تعمل.


وهنا يبدأ التحول من التخطيط إلى التطبيق الفعلي.
