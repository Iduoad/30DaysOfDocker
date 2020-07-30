# 30 Days of Docker - Day 10

<div dir="rtl">
   دائما مع Dockerfiles .. كاينين 3 ديال Commands لي لي تايمكنونا نexecutew commands، لي هوما RUN و CMD و ENTRYPOINT .
</div>

<div dir="rtl"><ul>
    <li>    بالنسية لRUN الCommand تاتexecuta وسط الimage براسها، يعني منين تاندير docker build .</li>
</ul></div>

    # dockerfile
    ...
    RUN apt-get update && apt-get install curl
    ...
    # ---

<!-- -->

    # this will be executed when we'll call this
    $ docker build -t devc:rabat .

<div dir="rtl"><ul>
    <li>     بالنسبة لCMD و ENTRYPOINT تايexecutaw منين تانرانيو container ديالنا. يعني Docker run</li>
</ul></div>

    # dockerfile
    ...
    CMD curl Devc.com
    ...
    # ---

<!-- -->
    # this will be executed when we'll call this
    $ docker run devc:rabat

<div dir="rtl">
    حاجة أخرى مهمة هي أنن هاذ الكوماندس ممكن ياخدو 2 أشكال
    <ul>
        <li>    الEXEC Form و هنا تانعطيو الbinary لي بغينا نexecutew مع باراميترز ديالو على شكل array و docker تايمشي يقلب في الPATH و تايقضي الغرض</li>
    </ul>
</div>

    # dockerfile
    ...
    RUN ["apt", "install", "-y", "curl"]
    CMD ["/bin/curl", "https://devc.com"]
    ...

<div dir="rtl">
    <ul>
        <li>    الSHELL form لي تانعطيو فيها commands لي بغينا على شكل string هاذ المرة و Docker تايدوزهم للشيل الشهير sh باش يexecutehom </li>
    </ul>
    هاذ الثانية تاتنفعنا ايلا بغينا نستعملو شي خاصيات ديال الشيل بحال && و || و pipes ....
</div>

    # dockerfile
    ...
    RUN apt install -y curl
    # is equivalent to
    CMD ["/bin/sh", "-c", "apt install -y curl"]


---
<div dir="rtl">ملاحظات:
    <ul>
        <li>بالنسبة لshell form، في حالة CMD أو ENTRYPOINT الpid 1 تايكون هو sh و هاذشي لي تايمنعنا من أننا نتواصلو مع الexecutable ديالنا مباشرة باستعمال Unix Signals يعني ايلا كان عندك شي program تاي...handle CTRL+C or CTRL+Z بشي طريقة في شكل من الأحسن تستعمل EXEC form .. حيت في هاذ الحالة غادي يكون sh حاجز بينك و بين البروكّرام ديالك و هو لي غادي يتكلف ب signals.</li>
        <li>كاين فرق بين CMD و ENTRYPOINT غادي نهضرو عليه المرة الجاية</li>
    </ul>   
</div>