# FRP Protocol Tester

تستر چندپروتکله برای بررسی وضعیت تانل ریورس **frp** بین سرور ایران و خارج.

### پروتکل‌های پشتیبانی‌شده

| پروتکل       | توضیح                          | لایه   |
|--------------|--------------------------------|--------|
| **TCP**      | پایدار و پیش‌فرض               | TCP    |
| **KCP**      | مناسب شبکه‌های پرتأخیر و پرلگ  | UDP    |
| **QUIC**     | مدرن، مالتی‌پلکسینگ قوی        | UDP    |
| **WebSocket**| مناسب عبور از فایروال و CDN    | TCP    |

---

## ویژگی‌ها

- تشخیص خودکار سرور ایران / خارج
- نصب ایزوله باینری‌های frp (بدون تداخل با نسخه‌های موجود)
- همگام‌سازی نسخه کلاینت و سرور
- باز کردن خودکار پورت‌ها روی UFW
- پشتیبانی از یوزر غیر روت (با `sudo`)
- پورت‌های رندوم و غیرمعمول
- خروجی رنگی و خوانا
- مناسب سرورهای کند ایران (دارای مکث بین مراحل)

---

## پیش‌نیازها

روی **سرور خارج** اجرا شود:

```bash
apt update
apt install -y curl wget tar netcat-openbsd sshpass openssl
```

---

## نصب و اجرا

### روش سریع

```bash
bash <(curl -sSL https://raw.githubusercontent.com/USERNAME/frp-protocol-tester/main/frp-tester.sh) \
  --iran-host IP_OR_DOMAIN \
  --iran-port 22 \
  --iran-user root \
  --iran-pass 'PASSWORD'
```

### روش دستی

```bash
wget -O frp-tester.sh https://raw.githubusercontent.com/USERNAME/frp-protocol-tester/main/frp-tester.sh
chmod +x frp-tester.sh

./frp-tester.sh \
  --iran-host 2.144.x.x \
  --iran-port 22 \
  --iran-user cloud-admin \
  --iran-pass 'YourPassword'
```

---

## پارامترها

| پارامتر         | توضیح                        | پیش‌فرض |
|-----------------|------------------------------|---------|
| `--iran-host`   | آی‌پی یا دامنه سرور ایران    | —       |
| `--iran-port`   | پورت SSH                     | `22`    |
| `--iran-user`   | نام کاربری SSH               | `root`  |
| `--iran-pass`   | رمز عبور SSH                 | —       |

---

## نمونه خروجی

```
╔════════════════════════════════════════════╗
║           FINAL TEST RESULTS               ║
╚════════════════════════════════════════════╝

  PROTOCOL       STATUS
  ────────────────────────────
  TCP            ✔  SUCCESS
  KCP            ✔  SUCCESS
  QUIC           ✔  SUCCESS
  WebSocket      ✔  SUCCESS
```

---

## ساختار پروژه

```
frp-protocol-tester/
├── frp-tester.sh          # اسکریپت اصلی
├── README.md              # مستندات انگلیسی
└── README-fa.md           # مستندات فارسی
```

---

## نکات مهم

1. اسکریپت باید از **سرور خارج** اجرا شود.
2. باینری‌های frp در مسیر زیر ذخیره می‌شوند و با نسخه‌های سیستم تداخل ندارند:
   ```
   /opt/frp_tester/bin/
   ```
3. در صورت فعال بودن UFW، پورت‌های مورد نیاز به‌صورت خودکار باز می‌شوند.
4. بین راه‌اندازی سرور ایران و شروع تست‌ها ۸ ثانیه مکث وجود دارد (مناسب سرورهای کند).

---

## مجوز

MIT License
