# SABIPANEL

یک پنل یکپارچه، واکنش‌گرا و دو‌زبانه برای مدیریت کاربران، دسترسی‌ها، اشتراک‌ها، نودها، Workerها، اسکنرها و اتوماسیون تلگرام.

## امکانات

- داشبورد مدیریتی فارسی و انگلیسی با حالت روشن و تاریک
- مدیریت کاربران، گروه‌ها، سهمیه‌ها و تاریخ انقضا
- صفحهٔ اختصاصی کاربر، لینک‌های اشتراک و QR Code
- مدیریت نودها، Workerها، همگام‌سازی و پایش سلامت
- ابزارهای بررسی IP، دامنه، SNI و TCP
- ربات مدیریت کانال و ربات فروش تلگرام
- پشتیبان‌گیری، بازیابی و ثبت رویدادها
- سازگار با VPS، Docker و Railway

## اجرای سریع با Docker

```bash
docker build -t sabipanel .
docker run --name sabipanel -p 8080:8080 -v sabipanel-data:/data sabipanel
```

سپس نشانی زیر را باز کنید:

```text
http://localhost:8080/sabi
```

## نصب روی سرور لینوکس

```bash
curl -fsSL https://raw.githubusercontent.com/sabi-karami/SABIPANEL/main/start.sh | bash
```

فرمان‌های مدیریتی:

```bash
sabipanel info
sabipanel status
sabipanel start
sabipanel stop
sabipanel restart
sabipanel update
sabipanel logs
```

## استقرار روی Railway

1. این مخزن را به یک پروژهٔ جدید Railway متصل کنید.
2. اجازه دهید Railway با `Dockerfile` موجود پروژه را بسازد.
3. پورت سرویس را روی `8080` قرار دهید.
4. یک دامنهٔ عمومی ایجاد کرده و برنامه را باز کنید.

## متغیرهای نصب

| متغیر | مقدار پیش‌فرض | کاربرد |
|---|---|---|
| `SABI_APP_DIR` | `/opt/SABIPANEL` | مسیر نصب |
| `SABI_REPO` | مخزن SABIPANEL | منبع به‌روزرسانی |
| `SABI_BRANCH` | `main` | شاخهٔ استقرار |
| `SABI_INSTALLER_URL` | فایل `start.sh` مخزن | نشانی نصب‌کننده |
| `SABI_UV_VERSION` | `0.12.9` | نسخهٔ uv |

اطلاعات حساس را داخل مخزن ذخیره نکنید و برای آن‌ها از متغیرهای محیطی یا Secretهای سرویس میزبان استفاده کنید.

## مسیرهای اصلی

```text
/sabi                 پنل اصلی
/login                ورود مدیر
/dashboard            داشبورد
/p/<key>              صفحهٔ اختصاصی کاربر
/api/sub/<key>        خروجی اشتراک
/healthz              بررسی سلامت سرویس
```

## توسعه

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python main.py
```

در Windows PowerShell، فعال‌سازی محیط مجازی با `.venv\Scripts\Activate.ps1` انجام می‌شود.

## ساختار پروژه

```text
SABIPANEL/
├── main.py
├── static/
├── worker/
├── data/
├── notif/
├── start.sh
├── Dockerfile
└── railway.toml
```

SABIPANEL با تمرکز بر پایداری، مدیریت ساده و تجربهٔ کاربری یکدست طراحی شده است.
