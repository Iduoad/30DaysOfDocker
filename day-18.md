# 30 Days of Docker - Day 18

<div dir="rtl">
اليوم غادي نكملوا الهضرة على Dockerfiles و هاذ المرة غادي نهضروا على package managers و كيفاش نستعملوهم بطريقة مزيانة في Dockerfiles <br>

كيفما قلنا قبل في اليوم 17 docker تايخبي Images على شكل immutable layers و أننا مخاصناش نكثروا الlayers باش نتفاداو نزيدوا الحجم ديال Images ديالنا.
حاجة آخرى هي خاصنا نحاولوا ما أمكن نحديوا Temporary Files بحال Build tools في layer في زدناهم، حيت كيفما قلنا قبل ايلا مشاو تابقاو ماغاديش يمكن نمسحوهم في شي Layer من بعد.
</div>

    RUN apt update && apt install -y git && git clone https://github.com/DevC_Rabat/DevC.git /DevC
    WORKDIR /DevC
    RUN chmod u+x install.sh && ./install.sh

<div dir="rtl">
في المثال لي داز عندنا واحد المشكل .. ال Image ديالنا غادي يكون فيها git و الSource Code ديالنا لي حنا مامحتاجينهمش أصلا في Final Image و واخا نمسحوهم في Layer من بعد ماغاديش 
غير غادي يتخباو و غادي يبقى الحجم ديال Image كبير.
</div>

<div dir="rtl">
بحال هاذ المشاكل تايتعاودوا بزاف مع Package Managers .. نشوفوا شي techniques باش نتفاداوهم في كل Package manager
مشكل الupdate ديال الpackage list في layer بوحدها

    RUN apt-get update 
    RUN apt-get install -y php

</div>

<div dir="rtl">
بالاضافة لأنه غادي تزاد عندنا layer إضافية .. منين تانديرو apt-get update في layer بوحدها، الpackage list ماغاديش يبقى يتبدل بين Docker builds واخا نبدلوا packages .. حيت هاذشي الlayer ماغاديش تبدل و Docker غادي يبقى ديما يجبدها من الcache ديالو.
تحديد الversions ديال packages<br>

من الأحسن دائما نديروا versions ديال packages لي تانآنسطاليو و نتفاداو Default version لي غادي ينقصوا من Visibility ديالنا و غادي يخليونا ماعارفينش شنو كاين في image ديالنا

    RUN apt-get update && apt-get install -y php7.3 git=2.1.3

</div>

<div dir="rtl">
نستعملوا الversions اللخرين ديال Distributions
النسخ القدام منين تاينديرو update لل package cache تايضطروا يتيليشارجيوا أكثر من الversion الجداد ..
نتفاداو الpackages الزايدين
في الimages المبنيين فوق من debian ممكن نقولو ل apt مايتيليشاجيش ال recommended packages

    RUN apt-get update && apt-get install -y --no-install-recommends php7.3

</div>

<div dir="rtl">
نحيدوا package list و package cache في نفس الlayer
باش نديروا هاذشي في debian

RUN apt-get update && apt-get install -y --no-install-recommends php7.3 && rm -rf /var/lib/apt/lists/* && apt-get clean
في أغلب الofficial base images ديال debian و ubuntu ال apt-get clean تاتدار أوتوكاتيطيا
باش نديروا هاذشي في redhat-based distros

    RUN yum -y php && rm -rf /var/cache/yum
</div>

في البوسط الجاي غادي نهضروا على كيفاش ننقصوا من size ديال image أكثر في Debian 