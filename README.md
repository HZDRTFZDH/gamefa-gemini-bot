# Gamefa Bot — Gemini 5-Key Failover/Rotation + Railway

این نسخه از Gamefa از Gemini API استفاده می‌کند و تا ۵ کلید Gemini را پشتیبانی می‌کند.

## Variables

Required:
- BOT_TOKEN
- ADMIN_ID
- GEMINI_API_KEY_1 ... GEMINI_API_KEY_5 (حداقل یکی)
- CHANNEL_ID (اختیاری؛ پیش‌فرض @Gamefa_official)

Optional:
- GEMINI_MODEL=gemini-2.5-flash
- GEMINI_EMBEDDING_MODEL=gemini-embedding-001

## رفتار ۵ کلیدی

- درخواست‌ها بین کلیدها به‌صورت چرخشی توزیع می‌شوند.
- خطاهای rate limit/quota/temporary باعث cooldown همان کلید می‌شوند و کلید بعدی امتحان می‌شود.
- کلید نامعتبر به‌صورت موقت از pool خارج می‌شود.
- پس از موفقیت، rotation از کلید بعدی ادامه پیدا می‌کند.
- GEMINI_API_KEY به‌عنوان fallback تک‌کلیدی نیز پذیرفته می‌شود.

نکته: چند API key در یک Google Cloud Project لزوماً سهمیه را چند برابر نمی‌کند؛ محدودیت‌های rate معمولاً در سطح project اعمال می‌شوند. برای افزایش واقعی ظرفیت، باید پروژه‌ها/سهمیه‌های مستقل داشته باشید و شرایط Google را رعایت کنید.

## Railway

1. فایل‌ها را در ریشه repository قرار بده.
2. در Railway از GitHub deploy کن.
3. در Variables، کلیدها را با نام‌های GEMINI_API_KEY_1 تا GEMINI_API_KEY_5 وارد کن.
4. هیچ API key را داخل GitHub commit نکن.
5. Procfile خودش `worker: python bot.py` را اجرا می‌کند.
