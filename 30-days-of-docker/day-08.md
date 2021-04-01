# 30 Days of Docker - Day 8

<div dir="rtl">
   كمالة على ذاكشي ديال COPY و ADD .<br>
   بزاف ديال المرات تانكونوا بغينا نكوبييو شي ملفات وبغيناهم يبانو بشي USER:GROUP معينين و هنا كاينين حلول لي بديهية
</div>

    # Solution 1
    COPY ./devC /app
    RUN chmod devc:devc
    # Solution 2
    USER devc:devc

<!-- -->
    
    COPY ./devC /app

<div dir="rtl">
   هاذ الحلول خدامة و لكن ماشي optimal خاصة الأول و غادي تزيد الحجم و الشكل ديال image ديالنا شوية .<br>
   الحل هو نستعملوا غير COPY
</div>

    COPY --chown devc:devc ./devC /app