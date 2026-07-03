ممتاز. الآن نصل إلى أهم وثيقة في المشروع كله. أي خطأ هنا سيؤثر على التطبيق بالكامل، لذلك سأصمم قاعدة البيانات كما لو أنها ستخدم مختبرًا طبيًا لسنوات.


---

04_Database_Design.md

معلومات الوثيقة

الحقل	القيمة

قاعدة البيانات	SQLite
ORM	Drift
الإصدار	1.0
نوع التطبيق	Offline First
المنصة	Flutter Android



---

فلسفة التصميم

تم تصميم قاعدة البيانات وفق المبادئ التالية:

تطبيع البيانات (Normalization).

عدم تكرار المعلومات.

سرعة البحث.

سهولة التوسع.

سهولة النسخ الاحتياطي.

سلامة العلاقات.



---

الجداول الرئيسية

1. users

الغرض

تخزين مستخدمي التطبيق.

الحقول

id
username
password_hash
full_name
role
phone
created_at
updated_at
is_active


---

2. patients

الغرض

بيانات المرضى.

الحقول

id
patient_number
full_name
gender
birth_date
age
phone
email
address
blood_group
doctor_id
notes
photo
created_at
updated_at


---

3. doctors

الغرض

بيانات الأطباء.

الحقول

id
name
specialization
phone
email
address
notes
created_at
updated_at


---

4. test_categories

الغرض

تصنيف الفحوصات.

مثال

Hematology

Chemistry

Hormones

Serology

Microbiology


الحقول

id
name
description


---

5. laboratory_tests

الغرض

الفحوصات.

الحقول

id
category_id
code
name
price
unit
normal_min
normal_max
critical_min
critical_max
description


---

6. reports

الغرض

التقرير الرئيسي.

الحقول

id
report_number
patient_id
doctor_id
report_date
status
notes
total_price
created_by
created_at
updated_at


---

7. report_items

الغرض

نتائج الفحوصات.

الحقول

id
report_id
test_id
result
unit
reference_range
flag
notes


---

8. laboratory_settings

الغرض

بيانات المختبر.

الحقول

id
lab_name
lab_logo
phone
email
address
website
currency
language
theme


---

9. attachments

الغرض

المرفقات.

الحقول

id
patient_id
report_id
file_name
file_path
file_type
created_at


---

10. activity_logs

الغرض

سجل العمليات.

الحقول

id
user_id
action
table_name
record_id
description
created_at


---

11. backups

الغرض

إدارة النسخ الاحتياطية.

الحقول

id
file_name
file_size
created_at
notes


---

العلاقات

Doctor
│
├───────────────┐
│               │
▼               ▼

Patients      Reports
                  │
                  │
                  ▼

            Report Items
                  │
                  ▼

          Laboratory Tests
                  │
                  ▼

          Test Categories


---

الفهارس (Indexes)

سنضيف فهارس على:

patient_number

phone

report_number

doctor_name

test_name

created_at

لتحسين سرعة البحث.


---

القيود

Patient Number

Unique


---

Username

Unique


---

Report Number

Unique


---

Foreign Keys

مفعلة بالكامل.


---

استراتيجية حذف البيانات

لن نحذف البيانات مباشرة.

بدلاً من ذلك

is_deleted

deleted_at

وبذلك يمكن استعادتها.


---

البحث

سيكون البحث داخل:

الاسم.

الهاتف.

رقم التقرير.

رقم المريض.

الطبيب.

الفحص.



---

الصور

لن تحفظ داخل قاعدة البيانات.

سيكون المسار فقط.

مثال

/storage/emulated/0/LabApp/patients/1001.jpg


---

التقارير PDF

سيتم حفظها داخل

Documents/Lab Reports/


---

النسخ الاحتياطي

سيتم ضغط:

database.db

+

images/

+

reports/

داخل ملف واحد.


---

استراتيجية الترقيم

رقم المريض

P000001


---

رقم التقرير

R000001


---

رقم الفاتورة

INV000001


---

الأداء

قاعدة البيانات مصممة لتحمل:

أكثر من 100 ألف مريض.

أكثر من مليون نتيجة.

آلاف التقارير.

بحث سريع.



---

الأمان

كلمات المرور لن تحفظ كنص صريح، بل ستخزن بشكل مُجزأ (Hash) مع إضافة Salt.

سيتم تشفير النسخ الاحتياطية اختياريًا.


---

ملاحظات مهمة

بعد مراجعة المشروع الأصلي، أرى أن هذه البنية أكثر مرونة وتسمح بإضافة ميزات مستقبلية مثل:

مزامنة سحابية اختيارية.

دعم أكثر من مختبر.

صلاحيات متعددة.

تطبيق iOS.

إصدار ويب.


قبل أن نكتب أول سطر كود

أقترح إضافة وثيقتين أساسيتين أخريين، لأنهما ستجعلان التنفيذ أسرع وأكثر احترافية:

1. 05_Project_Architecture.md: تحدد بنية المشروع في Flutter (المجلدات، الطبقات، ومسؤولية كل جزء).


2. 06_UI_UX_Design_System.md: تحدد نظام التصميم بالكامل (الألوان، الخطوط، الأزرار، البطاقات، الهوية البصرية، وقواعد تصميم الشاشات).



بعد اعتماد هاتين الوثيقتين، سنبدأ مباشرة بإنشاء مشروع Flutter وكتابة الكود، وسيكون لدينا مرجع واضح لكل قرار هندسي وتصميمي أثناء التطوير.
