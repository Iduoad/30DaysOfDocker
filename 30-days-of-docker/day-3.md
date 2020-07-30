# 30 Days of Docker - Day 3

<div dir="rtl">
    في نفس السياق ديال docker ps عاوتاني، ممكن تفيلتري المحتوى ديال docker ps بلا grep بلا والو غير ب filter-- .<br>
    هاذ اللعيبة تاتنفع عاوتاني في Debugging و حتى منين تاتبغي تمسح container لي مابقيتيش بغيتيهم و ممكن تخدمها مع format-- .
</div>

<div dir="rtl"><ul>
    <li>شي مرات تاتطلع ليك شي error و تاتبقى تصايب بزاف ديال containers باش تحاول تحلها، و منين تاتسالي و تايخدم ذاكشي تاتلقى بزاف ديال containers ماعندك ماتدير بيهم .. يكفي أنك تعرف الأول لي صايبتي و تخلي كلشي ل filter--</li>
</ul></div>

    $ docker rm -f $(docker ps -aq --filter="since=66bf51ac5a4b")

<div dir="rtl"><ul>
    <li>ايلا صايبنا شي image سميناها DevC لي تاتexecute commands معينين، و بغينا نعرفو containers لي كراشاو بسبب أن الكومند غالطة يعني error code = 127</li>
</ul></div>

    $ docker ps -a -f "exited=127" -f="ancestor=DevC" --format "{{.ID}} {{.Command}}"

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>التصويرة فيها الفلترز لي ممكن نستعملوهم</li>
    </ul>
    <p align="center">
        <a href="https://docs.docker.com/engine/reference/commandline/ps/#formatting">
            <img alt="filters" src="images/docker-ps-filtering.png"/>
        </a>
    </p>   
</div>