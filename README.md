# توزيع APK عبر GitHub Releases

مستودع لنشر تطبيقات Android (APK) مع **رابط تنزيل ثابت** يُحدَّث تلقائياً عند كل إصدار جديد، مع الاحتفاظ **باسم الملف الأصلي** عند التنزيل.

> **المستودع الحالي:** `sibhialnajjar/employee_apk`  
> **الرابط الثابت:** https://sibhialnajjar.github.io/employee_apk/

---

## المحتويات

1. [نظرة عامة](#نظرة-عامة)
2. [هيكل المشروع](#هيكل-المشروع)
3. [المتطلبات](#المتطلبات)
4. [إعداد مستودع جديد (لتطبيق المتاجر)](#إعداد-مستودع-جديد-لتطبيق-المتاجر)
5. [طريقة نشر إصدار جديد](#طريقة-نشر-إصدار-جديد)
6. [الملفات الكاملة للنسخ](#الملفات-الكاملة-للنسخ)
7. [استكشاف الأخطاء](#استكشاف-الأخطاء)

---

## نظرة عامة

### ماذا يفعل هذا النظام؟

| الميزة | الوصف |
|--------|--------|
| رابط ثابت | نفس الرابط يعمل دائماً ولا يحتاج تغييراً عند كل إصدار |
| تنزيل مباشر | عند النقر يبدأ تنزيل APK فوراً |
| اسم الملف الأصلي | يُنزَّل الملف بنفس الاسم الذي رفعته (مثل `2.1.0.apk`) |
| تحديث تلقائي | عند نشر Release جديد يُحدَّث الرابط تلقائياً دون تدخل يدوي |

### كيف يعمل؟

```
نشر Release جديد (مثل v2.1.0) + رفع APK بأي اسم
        ↓
GitHub Actions يعمل تلقائياً
        ↓
ينسخ APK إلى ريليز خاص اسمه "latest"
        ↓
صفحة GitHub Pages تقرأ آخر ملف من API
        ↓
المستخدم يضغط الرابط الثابت → يُنزَّل آخر نسخة بالاسم الأصلي
```

### الروابط المهمة

| الرابط | الاستخدام |
|--------|-----------|
| `https://OWNER.github.io/REPO/` | **الرابط الثابت للمشاركة** مع المستخدمين |
| `https://github.com/OWNER/REPO/releases` | إدارة الإصدارات |
| `https://github.com/OWNER/REPO/releases/download/vX.X.X/file.apk` | رابط إصدار محدد (يتغير مع كل نسخة) |

---

## هيكل المشروع

```
.
├── .github/
│   └── workflows/
│       └── update_latest.yml    # Workflow التحديث التلقائي
├── docs/
│   └── index.html               # صفحة التنزيل الثابتة (GitHub Pages)
└── README.md
```

> **ملاحظة:** ملفات APK **لا تُحفظ** داخل المستودع (حجمها يتجاوز حد GitHub 100MB). التوزيع يتم عبر **GitHub Releases** فقط.

---

## المتطلبات

- حساب GitHub
- مستودع عام (Public) أو خاص مع صلاحيات Actions
- تفعيل **GitHub Actions** (مفعّل افتراضياً)
- تفعيل **GitHub Pages** من مجلد `/docs`

---

## إعداد مستودع جديد (لتطبيق المتاجر)

اتبع الخطوات التالية لإنشاء نفس الإعداد في مستودع تطبيق المتاجر.

### الخطوة 1: إنشاء المستودع

1. أنشئ مستودعاً جديداً على GitHub (مثل `store_apk`)
2. استنسخه محلياً أو أنشئ الملفات مباشرة على GitHub

### الخطوة 2: إنشاء الملفات

أنشئ الملفات التالية بنفس المحتوى الموجود في قسم [الملفات الكاملة للنسخ](#الملفات-الكاملة-للنسخ)، مع تعديل:

| القيمة | مثال (الموظفين) | مثال (المتاجر) |
|--------|-----------------|----------------|
| `OWNER` | `sibhialnajjar` | `sibhialnajjar` |
| `REPO` | `employee_apk` | `store_apk` |

### الخطوة 3: تفعيل GitHub Pages

1. اذهب إلى **Settings** → **Pages**
2. اختر **Source:** `Deploy from a branch`
3. اختر **Branch:** `main` و **Folder:** `/docs`
4. اضغط **Save**
5. انتظر 1–2 دقيقة حتى يصبح الرابط جاهزاً:
   ```
   https://OWNER.github.io/REPO/
   ```

### الخطوة 4: أول تشغيل للـ Workflow

بعد رفع الملفات ونشر أول Release:

1. اذهب إلى **Actions** → **Update Latest APK**
2. اضغط **Run workflow** → **Run workflow** (مرة واحدة فقط إذا لم يُنشأ ريليز `latest` بعد)

> بعد ذلك، كل Release جديد يُحدَّث تلقائياً.

### الخطوة 5: التحقق

1. افتح الرابط الثابت: `https://OWNER.github.io/REPO/`
2. يجب أن يبدأ تنزيل APK فوراً
3. تحقق من وجود ريليز `latest` في قسم Releases

---

## طريقة نشر إصدار جديد

### الخطوات (لكل إصدار)

1. اذهب إلى **Releases** → **Draft a new release**
2. أنشئ **Tag** جديد (مثل `v2.1.0`)
3. اكتب عنواناً ووصفاً للإصدار
4. ارفع ملف **APK بأي اسم تريده** (مثل `store-v2.1.0.apk`)
5. اضغط **Publish release**

### ما يحدث تلقائياً

- يعمل Workflow **Update Latest APK**
- يُنشأ/يُحدَّث ريليز `latest` بنفس ملف APK
- الرابط الثابت يشير فوراً إلى الإصدار الجديد

### قواعد مهمة

| ✅ افعل | ❌ لا تفعل |
|---------|-----------|
| استخدم Tag بصيغة `v1.0.0` | لا تنشر ريليز باسم `latest` يدوياً |
| ارفع APK بأي اسم واضح | لا ترفع APK داخل المستودع (Git) |
| اضغط **Publish release** | لا تترك Release كـ Draft فقط |

---

## الملفات الكاملة للنسخ

### 1. `.github/workflows/update_latest.yml`

```yaml
name: Update Latest APK

on:
  release:
    types: [published]
  workflow_dispatch:

permissions:
  contents: write

jobs:
  update:
    runs-on: ubuntu-latest
    if: github.event_name == 'workflow_dispatch' || github.event.release.tag_name != 'latest'

    steps:
      - name: Download versioned APK from release
        env:
          GH_TOKEN: ${{ github.token }}
        run: |
          TAG="${{ github.event.release.tag_name }}"

          if [ -z "$TAG" ]; then
            TAG=$(gh release list --repo "${{ github.repository }}" --limit 10 \
              --json tagName -q '.[] | select(.tagName != "latest") | .tagName' | head -n 1)
          fi

          if [ -z "$TAG" ]; then
            echo "No release found"
            exit 1
          fi

          ASSET_NAME=$(gh release view "$TAG" --repo "${{ github.repository }}" \
            --json assets -q '.assets[] | select(.name | endswith(".apk")) | select(.name != "latest.apk") | .name' \
            | head -n 1)

          if [ -z "$ASSET_NAME" ]; then
            echo "No versioned APK found in release $TAG"
            exit 1
          fi

          echo "Using APK from release $TAG: $ASSET_NAME"
          echo "ASSET_NAME=$ASSET_NAME" >> "$GITHUB_ENV"

          mkdir -p dist
          gh release download "$TAG" --repo "${{ github.repository }}" \
            --pattern "$ASSET_NAME" --dir dist --clobber

      - name: Update stable latest release
        env:
          GH_TOKEN: ${{ github.token }}
        run: |
          if gh release view latest --repo "${{ github.repository }}" >/dev/null 2>&1; then
            gh release delete latest --repo "${{ github.repository }}" --yes
          fi

          gh release create latest "dist/$ASSET_NAME" \
            --repo "${{ github.repository }}" \
            --title "Latest" \
            --notes "رابط ثابت لآخر نسخة. يُحدَّث تلقائياً عند نشر أي إصدار جديد."
```

---

### 2. `docs/index.html`

> **مهم:** غيّر `OWNER` و `REPO` في السطر 7 إلى قيم مستودعك.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>جاري التنزيل...</title>
    <script>
        fetch('https://api.github.com/repos/OWNER/REPO/releases/tags/latest')
            .then(function (response) {
                if (!response.ok) throw new Error('release not found');
                return response.json();
            })
            .then(function (data) {
                var apk = data.assets.find(function (asset) {
                    return asset.name.endsWith('.apk');
                });
                if (!apk) throw new Error('apk not found');
                window.location.replace(apk.browser_download_url);
            })
            .catch(function () {
                document.getElementById('status').textContent = 'تعذر بدء التنزيل. حاول لاحقاً.';
            });
    </script>
</head>
<body>
    <p id="status">جاري التنزيل...</p>
</body>
</html>
```

**لتطبيق المتاجر** (مثال):

```html
fetch('https://api.github.com/repos/sibhialnajjar/store_apk/releases/tags/latest')
```

**لتطبيق الموظفين** (الحالي):

```html
fetch('https://api.github.com/repos/sibhialnajjar/employee_apk/releases/tags/latest')
```

---

### 3. قائمة التحقق السريعة للنسخ

```
□ إنشاء مستودع جديد
□ إضافة .github/workflows/update_latest.yml
□ إضافة docs/index.html (مع تعديل OWNER/REPO)
□ تفعيل GitHub Pages من /docs
□ رفع الملفات إلى main
□ نشر أول Release مع ملف APK
□ تشغيل Workflow يدوياً مرة واحدة (إن لزم)
□ اختبار الرابط الثابت
```

---

## استكشاف الأخطاء

### خطأ 404 عند فتح الرابط الثابت

| السبب | الحل |
|-------|------|
| GitHub Pages غير مفعّل | فعّله من Settings → Pages → `/docs` |
| ريليز `latest` غير موجود | شغّل Workflow يدوياً من Actions |
| `index.html` يشير لمستودع خاطئ | تأكد من OWNER/REPO في السطر 7 |

### فشل Workflow

| الخطوة الفاشلة | السبب | الحل |
|----------------|--------|------|
| Download APK | لا يوجد APK في الريليز | ارفع ملف `.apk` قبل النشر |
| Update latest release | صلاحيات ناقصة | تأكد من `permissions: contents: write` |
| لا يعمل تلقائياً | Release Draft | اضغط **Publish release** وليس Save draft |

### Workflow يظهر Failure لكن التنزيل يعمل

إذا نجحت خطوة **Update stable latest release** وفشلت خطوة أخرى قديمة (مثل حفظ ملف في Git)، تجاهلها إذا كان ريليز `latest` محدّثاً. الإعداد الحالي لا يحفظ ملفات في Git لتجنب هذه المشكلة.

### ملف APK أكبر من 100MB

لا ترفع APK داخل المستودع. استخدم **GitHub Releases** فقط — يدعم ملفات حتى 2GB.

---

## ملخص للفريق

| البند | القيمة |
|-------|--------|
| المستودع | `sibhialnajjar/employee_apk` |
| الرابط الثابت | https://sibhialnajjar.github.io/employee_apk/ |
| Workflow | `Update Latest APK` |
| التحديث | تلقائي عند Publish release |
| اسم التنزيل | نفس اسم الملف المرفوع |
| التشغيل اليدوي | مرة واحدة فقط عند الإعداد الأولي |

### لإنشاء نفس الإعداد لتطبيق المتاجر

1. أنشئ مستودع `store_apk` (أو أي اسم)
2. انسخ الملفين من هذا التوثيق
3. عدّل `OWNER/REPO` في `docs/index.html`
4. فعّل GitHub Pages
5. انشر أول Release

**الرابط الثابت لتطبيق المتاجر سيكون:**
```
https://sibhialnajjar.github.io/store_apk/
```
