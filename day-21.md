# 30 Days of Docker - Day 21

<div dir="rtl">
من بعد ماهضرنا على good practices ديال package management في dockerfiles دابا نهضروا على شي نضائح حول الستيل ديال dockerfile
أول حاجة و لي كانت حتى في البوسطات لي دازو هي نقسموا RUN Commands الطوال لعدة سطور مفرقين ب \&& أو \;

    RUN apk add --no-cache --virtual .build-deps autoconf gcc g++ make git && \
        git clone $REPO /app && \
        cd /app && \
        make && make install && \apk del .build-deps

أبعد من هاذشي ممكن في حالة package installation من الأحسن نديرو كل واحد في سطرو نرتبوهم Alphabetically

    RUN apk add --no-cache --virtual .build-deps \
        autoconf \
        g++ \
        gcc \
        git \
        make  

و أخيرا ايلا بغينا نزيدو شي سطر في الأول أو في الأخير ديال هاذ RUN غادي يخاصنا ضروري نبدلوه يعني و هاذشي غادي يخلق لينا مشكل ايلا كنا خدامين ب Git مداام أن git diff ديالنا غادي تطلع فيها أن السطر الأول تبدل واخا حنا زدنا فيه \ && في اﻷخير.

    RUN set -eux && \ # diff here
        apk add --no-cache --virtual .build-deps \ # and here
        autoconf \
        g++ \
        gcc \
        git \
        make && \ # diff here
        git clone $REPO # and here

الحل نأونكادريو هاذيك الRUN بcommands ماتايديرو والو بحال : .. لي ماتاتدير والو من غير أنها تاتexpand الparameters لي تانعطيوها.

    RUN : && \
        apk add --no-cache --virtual .build-deps \
        autoconf \
        g++ \
        gcc \
        git \
        make && \
        :

دابا ايلا زدنا شي سطر الdiff غادي يكون فيها غير السطر لي زدنا

    RUN : && \
        set -eux && \ # diff only here
        apk add --no-cache --virtual .build-deps \
        autoconf \
        g++ \
        gcc \
        git \
        make && \
        git clone $REPO # diff only here
        :
        
</div>