# 30 Days of Docker - Day 2

<div dir="rtl">
    في نفس السياق ديال docker ps، ايلا الفورما output ديال docker ps ماعجبكش ممكن تبدلو باستعمال format-- .<br>
هاذ اللعيبة تاتنفع في Debugging باش تشوف المعلومات لي عندك بيهم غرض فقط .
و خاصة في reports فين ممكن تجبد اللائحة ديالة containers بواحد الفورما معينة (فيها غير ذاكشي لي تايهم الفريق ديالك(ولا الكليان)، و تزيدها في report و تسيفطو ليهم.
</div>

<div dir="rtl"><ul>
    <li>باش تجبد الأسماء و CMD لي تإكزيكيتات ديال جميع container على شكل table : </li>
</ul></div>

    $ docker ps -a --no-trunc --format="table {{.Names}}\t{{.Command}}"

<div dir="rtl"><ul>
    <li>باش تجبد اللائحة ديال containers و ports ديالهم على وديت شي رابور :</li>
</ul></div>

    $ docker ps --format="- Container {{.Names}} with ID {{.ID}} is running on those ports {{.Ports}}" >> report.md

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>الكومند docker ps -a باش تجبد جميع containers حتى لي ماشي running</li>
        <li>ايلا كانت شي معلومة طويلة docker ps تاتاخد غير واحد العدد ديال الحروف و تاتدير truncate لداكي لي بقى و ايلا بغينا نمنعوها من هاذشي، يعني بغينا المحتوى كامل تانستعملوا no-trunc--</li>
        <li>اذيك << باش نزيدو المحتوى ديال docker ps في report في اللخر</li>
        <li>هاذ format-- تاتخدم <a href="https://golang.org/pkg/text/template">Go template syntax</a></li>
        <li>في التصويرة كاين شنو ممكن نجبدو بالضبط من format--</li>
    </ul>
    <p align="center">
        <a href="https://docs.docker.com/engine/reference/commandline/ps/#formatting">
            <img alt="--format" src="images/docker-ps-formatting.png"/>
        </a>
    </p>   
</div>