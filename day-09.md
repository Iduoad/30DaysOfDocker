# 30 Days of Docker - Day 9

<div dir="rtl">
   كيفما قلنا قبل، عموما كلما كان عدد commands في Dockerfile كلما أحسن، و السبب أن images تايكونوا على شكل طبقات layers و كل طبقة تاتكون النتيجة ديال شي command<br>
   في هاذ القضية كاينين 2 أنواع ديال Commands .. الcommands لي تايبدلو شي حاجة في Filesystem بحال RUN و COPY و هاذو تايخلقوا طبقات عندها حجم و الcommands لي تايبدلوا غير في Metadata بحال EXPOSE و ENTRYPOINT <br>
   باش نجبدو الطبقات لي كاينين في شي image و الحجم ديالهم و شنو command لي خلقاتهم كانستعملوا docker history
</div>

    $ docker history devC:latest

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>كيفاش تايخبي Docker الimages و كيفاش تاتعامل معاهم فيه بزاف مايتقال و ماكرهتش نديرو ليه شي حاجة بوحدو</li>
        <li>كاينين أدوات ديال كوميونيتي لي تايعطيو معلومات أكثر على الimages بحال Dive </li>
    </ul>   
</div>