# 30 Days of Docker - Day 19

<div dir="rtl">
في البوسط لي قبل هضرنا على كيفاش ننقصوا الحجم ديال Docker image و في هاذ البوسط غاذي نديرو واحد case study على Debian based images

أول حاجة هي package cache w package lists: <br>
منين تانديروا apt-get update تاتعمر تايجبد lists ديال الpackages كاملين لي كاينين في repositories لي كاينة في `/etc/apt/sources.list` و تايتيليشارجيهم ل `/var/lib/apt/lists/` و في نفس الوقت منين تانديروا `apt-get install` الpackages لي تايتيليشارجاو تايخبيهم apt في `/var/cache/apt/archives/` في حالة ما حتاجيناهم من بعد.
أول حاجة غانديروها هي غادي نتخلصو من هاذشي كامل من بعد مانساليو installation

    RUN apt-get update && \
        apt-get install -y --no-install-recommends \
        autoconf gcc g++ make git && \
        git clone $REPO /app && \    
        cd /app && \
        make && make install && \
        rm -rf /var/lib/apt/lists/*
        # apt-get clean will be executed automatically if the image is official 

باستعمال هاذشي جميع الfiles الزايدين لي غادي يزيدهم apt غادي يتمسحوا في نفس الlayer و هاكا غادي نقتاصدو بزاف ديال space في image ديالنا ..ال build Dependencies

في المثال لي داز آ جميع الpackage لي آنسطالينا ماغاديش نستعملوهم في production و آنسطاليناهم غير باش نBuild'ew آبليكاسيون ديالنا ..

يعني غادي يخاصنا نحيدوهم في الأخير .. أبسط طريقة هي نكوبييو هاذيم الليست كاملة و نديروها قدام واحد apt-get remove و لكن ايلا كانوا كتار و مفرقين على مراحل غادي تصعاب علينا 
القضية ..

الحل هو نستعملوا apt-mark لي تاتبدل لينا الاعدادات ديال ال packages اللي تانعطيوها .. لي تايهمنا من هاذ ااعدادات هوما manual و auto لي تايحددوا واش الpackage تآنسطالا manually أو أنه تآنسطالا automatically as some other package dependency .
    
و من بعد غادي نستعملوا `apt-get purge -y --auto-remove` لي تاتمسح جميع الpackages لي تآنسطالاو auto و مابقيناش محتاجيهم .. و النتيجة غادي تولي شي حاجة بحال هاكا.

    RUN apt-get update && \
    # Before the installation, Save the list of all manual packages to a variable
        savedAptMark="$(apt-mark showmanual)"&& \
    # Install
        apt-get install -y --no-install-recommends \
        autoconf gcc g++ make git && \
        git clone $REPO /app && \    
        cd /app && \
        make && make install && \
        rm -rf /var/lib/apt/lists/* && \
    # mark all the packages as auto    
        apt-mark auto '.*' > /dev/null && \
    # get the list of previously installed packages and mark them as manual
        [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark && \
    # Delete all the packages that are marked auto
        apt-get purge -y --auto-remove
    # apt-get clean will be executed automatically if the image is official

هنا قبل مانبداو لانسكالاسيون ديال build dependencies تانقيدوا لا ليست ديال packages لي أصلا كاينين .. من بعد تانآنسطاليو داكشي ديالنا و تانخدموا بيه و تاينماركيوه auto باش تمسحوا autoremove
    
ملاحظات:
    
- في المثال لي الفوق مادرتش واحد المرحلة مهمة لي هي نماركي dependencies ديال جميع binaries لي عندنا في image باش يبقاو خدامين 

```
find /usr/local -type f -executable -exec ldd '{}' ';' \
    | awk '/=>/ { print $(NF-1) }' \    
    | sort -u \
    | xargs -r dpkg-query --search \   
    | cut -d: -f1 \
    | sort -u \
    | xargs -r apt-mark manual 
```
    
السطر 1 تانقليو على binaries ديالنا و تانجبدو dependencies ديالهم ب ldd و في السطر 2 و 3 تانجبدو السميات ديالهم .so وتانرتبوهم و في السطر 4 و 5 و 6 تانقلبوا على السميات ديال package names و تانرتبوهم .. و في السطر الأخير تانماركيوهم manual

> ايلا بغيتي تتعمق أكثر ضرب طليلة على الريبو ديال docker official images في github
https://github.com/.../blob/master/7.4/buster/fpm/Dockerfile

</div>
