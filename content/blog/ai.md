+++
title = "شروع هوشمندسازی موآ برای ارائه نتایج بهتر"
date = "2024-03-23"
description = "افزودن مدل های هوش‌‌مصنوعی به موآ"
[taxonomies]
tags = ["MOA", "ai"]
+++
در حال حاضر موآ ۱۶۰ موتور جستجو با موضوعات مختلف و متنوع دارد که به طور پیشفرض فقط ۸۰ عدد از آنها فعال هستند ( بیشتر آنها هم در دسته هایی بلااستفاده در حال استفاده هستند )، این به این معناست که در صورتی که کاربر موتور های خود را شخصی سازی نکند فقط تعداد بسیار کمی از موتور های جستجو استفاده می‌شوند.

## اما راهکار چیست؟
راهکار ما هوشمند سازی لیست موتور های فعال موآ است. بذارید با یک مثال توضیح بدم:
تصور کنید در حال جستجو نام یک فیلم در موآ هستید، اگر در فضای خالی کنار صفحه ( در حالت میزکار ) پیشنهاد هایی برای ویدئو های مرتبط ببینید، کمک خوبی برای رسیدن به پاسخ جستجویتان نخواهد بود؟

برای چنین کاری اولید قدم کوچک کردن دسته‌بندی های اصلی و کاهش تعداد انهاست.
اکنون دسته بندی موآ شامل مواردی مثل عمومی، تصاویر، ویدئوها، اخبار،آوا،‌ نقشه، فناوری‌اطلاعات، مقالات، فایل ها، شبکه اجتماعی، لغت‌نامه‌ها، بسته‌ها، پرسش و پاسخ و دیگر می‌شود که غیر از پنج مورد اول باقی عملا بلااستفاده هستند.

برای بهبود این موضوع باید دسته های اصلی تنها عمومی، تصاویر، ویدئو‌ها، آوا، اخبار باشند و باقی موتور ها در دسته های فرعی
دانش
مسافرت
مالی
انجمن
برنامه نويسي
کامپیوتر
کتاب و مقاله
فایل
نرم افزار
شبکه اجتماعی
آب و هوا
فرهنگ لغت
ورزش
سرگرمی
موسیقی
تصاویر
اخبار
ویدئو
نقشه
خرید
دیگر
جای بگیرند.

# نحوه استفاده مناسب از دسته های فرعی
حال که موتور ها را به دسته‌های موضوعی فرعی بیشتر تفکیک کردیم نیاز است تا استفاده مناسبی از آنها کنیم.

برای این کار باید مثلا برای جستجو اردبیل نتایج دسته فرعی نقشه در کنار صفحه ( اکنون پیشنهاد های ویکی‌پدیا در آنجا قرار دارد ) نمایش داده شود.
یا برای جستجو آب و هوای اردبیل نتای دسته فرعی آب و هوا نمایش داده شود. اما این موارد به کنار صفحه ( سایدبار ) محدود نمی‌شود، مثلا در جستجو پیکاسو نتایج دسته اصلی تصاویر هم وارد نتایج دسته عمومی خواهند شد ( این ترکیب نتایج نباید به دسته عمومی محدود شود و در دسته های اصلی دیگر مثلا تصاویر هم کاربرد خواهند داشت )

# چطور می‌توان این کار را کرد؟
برای پیاده سازی همچین چیزی ساده ترین راهکار تشخیص کلیدواژه های اصلی در متن جستجو است. مثلا برای هر دسته فرعی یک لیست از کلیدواژه های مرتبط ایجاد شود و اگر یکی از اینها درون جستجو بود دسته فرعی مرتبط  با دسته اصلی ترکیب شود.
مثلا برای کامپیوتر کلیدواژه هایی مثل
کامپیوتر
نرم‌افزار
لپ تاپ
سخت افزار
نرم افزار های اداری
گرافیک
مبنا قرار گیرند. در این صورت با جستجو تاریخچه کامپیوتر نتایج خوبی دریافت خواهیم کرد، اما در جستجو چطور کامپیوتر خود را تمیز کنیم چه؟ اینجاست که به مشکل خواهیم خورد.
راهکار دوم استفاده از هوش مصنوعی است. یعنی استفاده از یک مدل اموزش دیده هوش مصنوعی برای تصمیم گیری که آیا یک جستجو به ترکیب دسته نیاز دارد یا نه و اگر نیاز دارد چه دسته ای؟

برای این کار در حال اموزش یک مدل طبقه بندی متن با [FastText](https://fasttext.cc/) هستیم. یک مدل طبقه‌بندی متن یک ورودی متنی دریافت و بر اساس موضوع مربوط به آن ( که قبلا درباره آن اموزش دیده است ) یک خروجی را پیشنهاد می‌دهد. به طور مثال مدلی با داده هایی با برچسب های تصویر، ویدئو، موسیقی اموزش دیده. زمانی که شما اهنگ مصطفی راغب را به عنوان ورودی به مدل می‌دهید با توجه به داده های اموزشی که قبل تر انها را دیده است برای شما خروجی موسیقی را پیشنهاد می‌دهد


با این توصیف ما نیاز به داده هایی ( متن جستجو های اینترنتی ) برای اموزش مدل داریم.
داده ها باید چند زبانه باشند و به تفکیک موضوع، اما به غیر از چند دیتاست کوچک نتوانستم داده بیشتری پیدا کنم ( که همان ها هم فقط انگلیسی و اذربایجانی بودند ) چون بیشتر دیتاست های طبقه بندی متن طبقه بندی احساسی بودند نه موضوعی، برای حل مشکل دست به دامان ارشیو جستجو های [گوگل ترندز](https://trends.google.com/trends/) شدم و داده های سال ۲۰۲۳ را دستی ( کپی و پیست کردن ) استخراج کردم و این بسیار بسیار خسته کننده و کند بود.
بعد از ان با جستجو دستی در بخش کاوش گوگل ترندز مقداری داده استخراج کردیم.
در مرحله بعد با نوشتن اسکریپت زیر :
```python
from pytrends.request import TrendReq
import random
import pandas as pd

def append_list_to_file(lst, file_path):
    with open(file_path, 'a') as file:
        for item in lst:
            file.write(str(item) + '\n')

def extract_values(dictionary: dict):
    for inner_dictionary in dictionary.values():
        return list(inner_dictionary.values())

def related_searches(kw_list):
    pytrends = TrendReq(hl='ar', tz=100)
    pytrends.build_payload(kw_list, timeframe='today 3-m')
    related_queries = pytrends.related_queries()
    return related_queries

line_number = 1

def get_line_from_file(file_name, line_number):
    try:
        with open(file_name, 'r', encoding='utf-8') as file:
            lines = file.readlines()
            if 0 < line_number <= len(lines):
                return lines[line_number - 1]
            else:
                return f"Error: Line number {line_number} is out of range."
    except FileNotFoundError:
        return f"Error: File '{file_name}' not found."


file_path = 'da.txt'
for t in range(0, 100):
    random_word = get_line_from_file(file_path, line_number)
    while True:
        try:
            kw_list = [random_word]
            related_searche = related_searches(kw_list)
            extract_value = extract_values(related_searche)
            append_list_to_file(extract_value, "exp.txt")
            break
        except Exception as e:
            print(f"An error occurred: {str(e)}")
            continue
```
یک دیکشنری کوچک از واژگان مربوط به هر موضوع در فایل da.txt ( هر خط یک واژه ) قرار داده و پس از اجرای این کد مقدار نسبتا خوبی در زمان کوتاه داده استخراج شد و با بخشی از دیتاست های عمومی قابل استفاده، جمعا ۱۱۳ هزار خط داده خام ( به زبان های اذربایجانی فارسی انگلیسی و کمی هم دیگر زبان ها ) جمع آوری شد.

مشکل بعد برچسب زدن هر یک از این ۱۱۳ هزار خط ( !!! ) است. برای حل این مشکل مقدار داده ها را کم تر کردم و اکنون حدود ۸ هزار خط برچسب خورده داریم ( که کافی نیست ) و برای قابل استفاده شدن باید با اسکریپ بالا برای هر دسته فرعی یک دیکشنری ۱۰ کلمه ای مربوط به مثلا موضوع نقشه ایجاد شود  و با اسکریپت بالا داده های مربوط استخراج و برچسب گذاری کرد . این کار با دو زبان فارسی و انگلیسی تکرار شود و خروجی برچسب گذاری شده برای ترین و استفاده اولیه مناسب خواهد بود.

اما الان به دلیل درخواست زیاد از طرف گوگل ترندز مسدود شدم و نیاز به کمک برای این کار دارم :)) اگر کسی دوست داره کمکی در این باره کنه، چه استخراج چه برچسب گذاری ( سخت نیست کمکتون می‌کنم) و یا پیشنهاد دیتاست عمومی یا هر کمک دیگه ای می‌تونید به ماستودون موآ ( در پاورقی سایت قرار دارد ) یا به من در تلگرام پیام دهید @moa_engine

و در پایان توضیح کوتاهی درباره حالت کلی داده های مورد نیاز بدم.
این یک بخش از داده هاست :
```
__label__knowledge یادگیری هوش مصنوعی
__label__knowledge یادگیری برنامه نویسی
__label__knowledge یادگیری زبان آلمانی
__label__knowledge سامانه یادگیری فرهنگیان
__label__knowledge آموزش زبان انگلیسی
__label__knowledge سامانه یادگیری هلال احمر
__label__knowledge مدیریت یادگیری هلال احمر
__label__knowledge آزمون سنجش دستاوردهای یادگیری
__label__knowledge سامانه یادگیری جمعیت هلال احمر
__label__knowledge نقش شبکه عصبی در یادگیری ماشینی
```
(برچسب ها برای نمونه هستند) هر ورودی جستجو یعنی هر چیزی که در اینترنت جستجو می‌شود در یک خط قرار گرفته و و قبل از آن متن "__label__" که نشانگر برچسب هر ورودی است قرار می‌گیرد و وابسته به موضوع هر ورودی یک یا چند برچسب بدون فاصله بعد از __label__ گذاشته خواهند شد.
برچسب ها باید از موارد زیر باشند
```
knowledge
travel
financial
forum
programming
computer
book-and-article
file
software
social-network
weather
dictionary
sport
entertainment
music
images
news
video
map
buy
none
```
یک مثال برای ورودی چند برچسبی ( برچسب ها نمایشی است. ) :
```
__label__knowledge __label__software یادگیری هوش مصنوعی

```


به زودی داده های کنونی را بر روی [گیتهاب موآ](https://github.com/moa-engine/) قرار خواهم داد این می‌تواند شروع خوبی برای کمک در برچسب گذاری داده ها باشد
