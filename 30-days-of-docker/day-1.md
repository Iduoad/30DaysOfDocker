# 30 Days of Docker - Day 1

<div dir="rtl">
    إيلا بغيتي تجبد آخر Containers صايبتي (docker create/run) ممكن تستعمل l- و n- ديال Docker ps ..
ممكن تخدم هاذ اللعيبة باش تمسح container لي صايبتي مأخرا:
</div>

<div dir="rtl"><ul>
    <li>باش تمسح آخر container :</li>
</ul></div>

    $ docker rm $(docker ps -ql)

<div dir="rtl"><ul>
    <li>باش تمسح آخر خمسة containers :</li>
</ul></div>

    $ docker rm $(docker ps -qn 5)

> <div dir="rtl">ملاحظة : docker ps -q باش تخرّج غير IDs ديال containers</div>