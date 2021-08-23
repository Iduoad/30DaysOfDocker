# 30 Days of Docker - Day 20

<div dir="rtl">
في البوسط لي قبل هضرنا على كيفاش ننقصوا الحجم ديال Docker image في Debian based images و في هاذ البوسط غادي نديرو case study آخرى على Alpine based images
ا Alpine linux هي واحد الdistribution صغيرة بزاااف مقارنة مع لاخرين و لي مديورة خصيصا للاستعمال في container images .
القضية هنا أسهل مادام package manager فيه features لي غادي ينفعونا ننقصوا من الحجم ديال الimage ديالنا من اللخر ..

ال package cache w package lists
الpackage manager ديال alpine سميتو apk .. فيه واحد الoption --no-cache لي تاتعطيني الامكانية نمسحوا الcache كامل من بعد الأنسطالاسيون.

    RUN apk add --no-cache autoconf gcc g++ make git 

ال build Dependencies

هاذ المرة عاوتاني القضية أسهل، باستعمال --virtual لي تاتعطينا الامكانية باش نصايبو named groups ديال الpackages لي ممكن نمسحو بيه من بعد جميع الpackages ب apk del

    RUN apk add --no-cache --virtual .build-deps autoconf gcc g++ make git && \
        git clone $REPO /app && \
        cd /app && \
        make && make install && \
        apk del .build-deps

</div>