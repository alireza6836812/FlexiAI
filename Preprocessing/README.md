# 1. General / Cross-modal preprocessing workflows

**1. Data ingestion and schema validation**

* توضیح: بررسی می‌کند داده ورودی با نوع و ستون‌های مورد انتظار سازگار باشد.
* Example: فایل CSV داری که ستون `age` باید عدد باشد اما بعضی مقادیر `"unknown"` هستند. در این مرحله:

  1. ستون بررسی می‌شود.
  2. مقادیر غیرعددی اصلاح یا حذف می‌شوند.
  3. مدل بعدی می‌تواند بدون خطا اجرا شود.

**2. Data profiling and exploratory analysis**

* توضیح: نگاه اولیه آماری و تصویری به داده برای فهم توزیع و کیفیت.
* Example: رسم histogram درآمد کاربران → متوجه skew شدید می‌شوی → تصمیم می‌گیری log-transform اعمال کنی.

**3. Missing data handling**

* توضیح: پر کردن یا مدیریت مقادیر گمشده.
* Example: ستون `age` ۱۰٪ مقدار ندارد. راه‌ها:

  * حذف ردیف → کاهش داده
  * پر کردن با median → عدد ۳۲ جایگزین NaN

**4. Outlier detection and treatment**

* توضیح: شناسایی داده‌های غیرواقعی یا پرت و اصلاح آن‌ها.
* Example: قد انسان: بیشتر ۱۵۰–۱۹۰، یک مقدار ۳۵۰ → حذف می‌شود.

**5. Noise reduction and smoothing**

* توضیح: حذف نوسانات تصادفی از داده.
* Example: داده دمای سنسور: `20.1, 20.3, 25.7, 20.2` → moving average → `20.2, 20.3, 20.4`

**6. Data normalization and scaling**

* توضیح: هم‌مقیاس‌سازی ویژگی‌ها.
* Example: height=150–190، income=1M–100M → StandardScaler → همه ویژگی‌ها در مقیاس مشابه

**7. Feature encoding**

* توضیح: تبدیل داده غیرعددی به عدد.
* Example: gender = {male, female} → 0/1 یا one-hot `[1,0], [0,1]`

**8. Feature transformation**

* توضیح: تغییر توزیع برای یادگیری بهتر.
* Example: log(price) برای داده توزیع نمایی.

**9. Feature selection**

* توضیح: حذف ویژگی‌های کم‌اثر.
* Example: ستون `user_id` هیچ کمکی نمی‌کند → حذف.

**10. Feature extraction**

* توضیح: ساخت ویژگی معنادار از داده خام.
* Example: صوت خام → MFCC → انرژی و فرکانس → مدل قابل استفاده

**11. Dimensionality reduction**

* توضیح: کاهش تعداد ویژگی‌ها با حفظ اطلاعات اصلی.
* Example: ۳۰۰ ویژگی ژنتیک → PCA → ۵۰ مؤلفه → ۹۵٪ اطلاعات حفظ می‌شود

**12. Data augmentation**

* توضیح: افزایش داده با تغییرات مصنوعی.
* Example: تصاویر گربه → flip, rotate → تعداد نمونه‌ها ۱۰ → ۱۰۰

**13. Train / Validation / Test splitting**

* توضیح: جدا کردن داده برای آموزش، تنظیم و ارزیابی.
* Example: ۱۰۰۰ نمونه → train=۷۰۰, validation=۱۵۰, test=۱۵۰

**14. Cross-validation preparation**

* توضیح: ارزیابی پایدارتر با چند تقسیم متفاوت.
* Example: ۵-fold cross-validation روی دیتاست کوچک

**15. Data leakage prevention**

* توضیح: جلوگیری از نشت اطلاعات آینده به آموزش.
* Example: scaler فقط روی train fit شود

**16. Class imbalance handling**

* توضیح: مقابله با تعداد نابرابر نمونه‌ها در کلاس‌ها.
* Example: fraud class=1٪ → SMOTE oversampling

**17. Pipeline orchestration**

* توضیح: اتصال تمام مراحل پیش‌پردازش به یک جریان تکرارپذیر.
* Example: sklearn Pipeline: scaling → PCA → model

---

# 2. Tabular data preprocessing workflows

**1. Data cleaning and type coercion**

* توضیح: اصلاح داده‌های غلط و اطمینان از نوع صحیح.
* Example: `"32 years"` → 32

**2. Categorical encoding workflows**

* توضیح: رمزگذاری متغیرهای دسته‌ای برای مدل.
* Example: city = {Tehran, Shiraz} → one-hot: `[1,0], [0,1]`

**3. Numerical scaling workflows**

* توضیح: مقیاس‌بندی ویژگی‌های عددی برای الگوریتم‌های حساس به مقیاس.
* Example: RobustScaler روی salary با outlier زیاد

**4. Mixed-type feature engineering**

* توضیح: ترکیب ویژگی‌های عددی و دسته‌ای برای ساخت ویژگی جدید.
* Example: age + job → risk_score

**5. Aggregation feature creation**

* توضیح: خلاصه‌سازی داده‌ها برای هر نمونه یا گروه.
* Example: mean purchase per user

**6. Interaction feature construction**

* توضیح: ترکیب دو ویژگی برای اثر متقابل.
* Example: age × income

**7. Sparse matrix preparation**

* توضیح: نمایش کارآمد داده پراکنده.
* Example: TF-IDF matrix از متن

**8. Feature pruning**

* توضیح: حذف ستون‌های کم‌اثر یا ثابت.
* Example: حذف ستون با variance = 0

---

# 3. Time-series preprocessing workflows

**1. Time index alignment**

* توضیح: هم‌تراز کردن داده‌ها با محور زمان.
* Example: یکی دقیقه‌ای، دیگری ثانیه‌ای → resample

**2. Missing timestamp interpolation**

* توضیح: پر کردن نقاط گمشده در زمان.
* Example: خطی بین دو مقدار موجود

**3. Trend / seasonality decomposition**

* توضیح: جدا کردن روند و الگوی فصلی.
* Example: فروش ماهانه = trend + seasonality

**4. Stationarity enforcement**

* توضیح: ایستا کردن سری زمانی برای مدل‌ها.
* Example: differencing قیمت سهام

**5. Sliding window generation**

* توضیح: تبدیل سری به نمونه‌های supervised.
* Example: ۳۰ روز گذشته → پیش‌بینی روز بعد

**6. Lag / lead feature creation**

* توضیح: افزودن ویژگی گذشته یا آینده نزدیک.
* Example: y(t−1), y(t−7)

**7. Rolling statistics extraction**

* توضیح: استخراج میانگین یا انحراف معیار متحرک.
* Example: rolling mean ۷ روزه

**8. Frequency-domain transformation**

* توضیح: تبدیل داده به فرکانس برای تحلیل.
* Example: FFT روی ECG

**9. Temporal train-test split**

* توضیح: جداسازی داده بدون shuffle.
* Example: آموزش ۲۰۲۰–۲۰۲۲، تست ۲۰۲۳

**10. Anomaly preprocessing**

* توضیح: آماده‌سازی برای تشخیص ناهنجاری.
* Example: حذف trend قبل از anomaly detection

---

# 4. Text / NLP preprocessing workflows

**1. Text cleaning and normalization**

* توضیح: حذف نویز و استانداردسازی متن.
* Example: حذف URL، emoji، علائم اضافی

**2. Tokenization**

* توضیح: شکستن متن به واحدهای کوچک (کلمه یا subword).
* Example: `"من عاشق گربه‌ها هستم"` → `["من","عاشق","گربه","ها","هستم"]`

**3. Case folding**

* توضیح: یکسان کردن حروف بزرگ و کوچک.
* Example: `"Apple"` → `"apple"`

**4. Stop-word removal**

* توضیح: حذف کلمات کم‌اطلاعی مثل `the`, `is`
* Example: `"من به مدرسه می‌روم"` → حذف `"به"` → `["من","مدرسه","می‌روم"]`

**5. Stemming and lemmatization**

* توضیح: کاهش کلمات به ریشه معنایی
* Example: `"دوست‌داشتنی"` → `"دوست‌داشت"`

**6. Vocabulary construction**

* توضیح: ساخت دیکشنری واژگان برای مدل
* Example: انتخاب top 30k frequent tokens

**7. Rare token handling**

* توضیح: مدیریت کلمات کم‌تکرار
* Example: کلمه‌ای که فقط یکبار آمده → `<UNK>`

**8. Padding and truncation**

* توضیح: هم‌طول کردن توالی‌ها برای مدل
* Example: جمله کوتاه با ۵ توکن → pad تا ۱۲۸، جمله طولانی → truncate

**9. N-gram generation**

* توضیح: ایجاد توالی چندکلمه‌ای برای حفظ context
* Example: `"machine learning is fun"` → bigrams: `["machine learning","learning is","is fun"]`

**10. TF-IDF transformation**

* توضیح: وزن‌دهی آماری کلمات برای مدل‌های کلاسیک
* Example: spam detection

**11. Embedding preparation**

* توضیح: تبدیل کلمات به بردار عددی معنادار
* Example: FastText embedding

**12. Language detection**

* توضیح: تشخیص زبان متن و فیلتر کردن غیرمطلوب
* Example: حذف متن غیرانگلیسی

**13. Text data augmentation**

* توضیح: افزایش داده با تغییر متن
* Example: synonym replacement → `"خوب"` → `"عالی"`

5. Image preprocessing workflows

(پردازش و آماده‌سازی تصاویر برای مدل‌های بینایی ماشین)

1. Image decoding and loading

توضیح: تبدیل فایل تصویری (JPEG, PNG) به ماتریس اعداد که مدل بتواند بفهمد.

Example: بارگذاری cat.jpg → numpy array (224,224,3) که هر پیکسل بین 0–255 است.

2. Resolution standardization

توضیح: یکسان‌سازی اندازه تصاویر برای ورودی مدل.

Example: تصاویر مختلف با سایز 300×400, 500×600 → resize همه به 224×224.

3. Aspect-ratio handling

توضیح: حفظ یا اصلاح نسبت طول به عرض تصویر.

Example: crop یا padding برای جلوگیری از کشیده شدن گربه در تصویر.

4. Pixel normalization

توضیح: تبدیل مقادیر پیکسل‌ها به بازه قابل قبول مدل.

Example: تقسیم همه پیکسل‌ها بر 255 → مقادیر 0–1.

5. Color space conversion

توضیح: تغییر فضای رنگ تصویر برای الگوریتم‌ها یا ویژگی‌ها.

Example: RGB → grayscale برای کاهش پیچیدگی و مصرف حافظه.

6. Noise reduction

توضیح: حذف نویز تصویر بدون از دست دادن جزئیات مهم.

Example: Gaussian blur برای تصاویر MRI.

7. Contrast enhancement

توضیح: بهبود کنتراست برای دید بهتر مدل.

Example: histogram equalization روی عکس سیاه‌وسفید.

8. Image augmentation

توضیح: تغییرات مصنوعی برای افزایش تنوع داده.

Example: rotate, flip, brightness change → از ۱۰۰ تصویر → ۱۰۰۰ تصویر.

9. Patch extraction

توضیح: بریدن نواحی کوچک تصویر برای مدل‌های patch-based.

Example: تصویر 224×224 → 16×16 patches برای ViT.

10. Mask generation

توضیح: تولید ماسک برای segmentation یا detection.

Example: تصویر گربه → ماسک دو بعدی که فقط گربه را سفید نشان می‌دهد، بقیه سیاه.

6. Video preprocessing workflows

1. Frame extraction

توضیح: استخراج فریم‌ها از ویدئو برای پردازش مدل.

Example: ویدئو 30fps → تبدیل به 300 فریم.

2. Temporal sampling

توضیح: کاهش تعداد فریم برای کاهش حجم یا محاسبات.

Example: هر ۱۰ فریم → یک فریم انتخاب شود.

3. Optical flow computation

توضیح: محاسبه حرکت بین فریم‌ها برای مدل‌های action recognition.

Example: شناسایی جهت حرکت دست در بازی ویدیویی.

4. Clip segmentation

توضیح: تقسیم ویدئو به کلیپ‌های کوتاه.

Example: ویدئو ۳ دقیقه‌ای → ۱۸ کلیپ ۱۰ ثانیه‌ای.

5. Motion stabilization

توضیح: حذف لرزش دوربین برای تحلیل بهتر حرکت.

Example: ویدئو موبایل هنگام راه رفتن → حذف jitter.

6. Spatio-temporal augmentation

توضیح: افزایش داده در فضا و زمان.

Example: crop spatial + time shift → افزایش تعداد نمونه‌ها.

7. Audio–video synchronization

توضیح: همگام‌سازی صدا و تصویر برای multimodal models.

Example: lipsync recognition → مطمئن می‌شویم فریم صوت و ویدئو همزمان است.

7. Audio and speech preprocessing workflows

1. Audio resampling

توضیح: یکسان‌سازی نرخ نمونه‌برداری برای تمام فایل‌ها.

Example: 44.1kHz → 16kHz برای مدل ASR.

2. Silence trimming

توضیح: حذف سکوت ابتدای فایل و انتها.

Example: فایل صوتی ۵ ثانیه با ۲ ثانیه سکوت → trimming → فقط صدای واقعی.

3. Noise reduction

توضیح: حذف نویز زمینه.

Example: spectral gating روی صدای ضبط شده در خیابان.

4. Signal normalization

توضیح: هم‌مقیاس‌سازی دامنه صدا.

Example: peak normalization → همه فایل‌ها دامنه بین -1 و 1.

5. Framing and windowing

توضیح: تقسیم سیگنال به فریم‌های کوچک برای استخراج ویژگی.

Example: 25ms frames با overlap 10ms.

6. Spectrogram generation

توضیح: تبدیل صوت به تصویر فرکانسی.

Example: log-mel spectrogram برای CNN صوتی.

7. MFCC extraction

توضیح: استخراج ویژگی گفتاری فشرده و مهم.

Example: MFCC → input ASR یا speaker recognition.

8. Pitch normalization

توضیح: نرمال‌سازی زیر و بمی صدا برای مدل مستقل از گوینده.

Example: همه صداها به همان محدوده pitch.

9. Audio augmentation

توضیح: تغییر مصنوعی صدا برای افزایش داده.

Example: time stretch, pitch shift → افزایش robustness.

8. Graph and network preprocessing workflows

1. Graph construction

توضیح: تبدیل داده به گراف (رأس‌ها و یال‌ها).

Example: user-item interaction → user nodes + item nodes + edges.

2. Node/edge feature engineering

توضیح: اضافه کردن ویژگی‌ها به گراف.

Example: node degree, edge weight.

3. Adjacency normalization

توضیح: نرمال‌سازی ماتریس مجاورت برای GCN.

Example: D^(-1/2) A D^(-1/2).

4. Subgraph sampling

توضیح: نمونه‌گیری زیرگراف برای مدل‌های بزرگ.

Example: neighbor sampling در GraphSAGE.

5. Graph coarsening

توضیح: کاهش اندازه گراف با حفظ ساختار اصلی.

Example: pooling nodes مشابه → graph کوچک‌تر.

6. Positional encoding

توضیح: اضافه کردن اطلاعات مکانی/مرکزی برای مدل.

Example: eigenvectors of Laplacian → node positions.

9. Multimodal preprocessing workflows

1. Modality-specific preprocessing

توضیح: هر مدالیته (صوت، تصویر، متن) را جدا پردازش می‌کنیم.

Example: CNN برای تصویر، BERT برای متن.

2. Cross-modal alignment

توضیح: هماهنگ‌سازی زمان یا نمونه‌ها بین مدالیته‌ها.

Example: caption ↔ frame video.

3. Missing modality handling

توضیح: وقتی مدالیته‌ای گم شده، fallback مناسب.

Example: متن موجود اما تصویر نیست → از embedding text استفاده می‌کنیم.

4. Fusion-ready formatting

توضیح: آماده‌سازی داده‌ها برای ترکیب مدالیته‌ها.

Example: concat embeddings قبل از input به مدل.

10. Label and target preprocessing workflows

1. Label cleaning

توضیح: حذف یا اصلاح برچسب‌های اشتباه.

Example: تصویر سگ ولی label=cat → اصلاح یا حذف.

2. Label encoding

توضیح: تبدیل برچسب به عدد.

Example: cat → 0, dog → 1.

3. Multi-label binarization

توضیح: نمایش چندبرچسبی به صورت باینری.

Example: [rock, jazz] → [1,0,1].

4. Soft label generation

توضیح: تولید برچسب احتمالی به جای ۰/۱.

Example: label smoothing → 0.9 و 0.1 به جای 1 و 0.

5. Target scaling

توضیح: مقیاس‌بندی خروجی‌های عددی برای مدل.

Example: StandardScaler روی y رگرسیون.

11. Dataset-level governance workflows

1. Bias and fairness auditing

توضیح: بررسی سوگیری داده‌ها بین گروه‌ها.

Example: Accuracy جداگانه برای مرد و زن → مطمئن شویم مدل عادلانه است.

2. Anonymization and masking

توضیح: حذف اطلاعات هویتی افراد.

Example: hash کردن user_id → ناشناس‌سازی داده‌ها.

3. Differential privacy

توضیح: حفظ حریم خصوصی آماری.

Example: افزودن نویز به gradients هنگام آموزش.

4. Dataset versioning

توضیح: نگهداری نسخه‌های مختلف dataset.

Example: DVC v1.2 برای track تغییرات.

12. Deployment-oriented preprocessing workflows

1. Training–serving skew prevention

توضیح: مطمئن شدن از یکسان بودن preprocessing آموزش و اجرا.

Example: reuse همان scaler ذخیره‌شده در inference.

2. Online vs offline preprocessing

توضیح: تمایز بین پردازش لحظه‌ای و آفلاین.

Example: feature از تاریخچه یک ماهه → batch processing، feature real-time → online.

3. Feature store integration

توضیح: ذخیره و بازیابی ویژگی‌ها از مخزن مرکزی.

Example: Feast → train و serving از یک منبع استفاده کنند.

4. Latency-optimized preprocessing

توضیح: کاهش زمان پردازش برای اجرای سریع مدل.

Example: حذف PCA هنگام inference → کاهش زمان prediction.
