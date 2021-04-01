# 30 Days of Docker - Day 4

<div dir="rtl">
    آخر لعيبة على الفيلترز و ذاكشي .. هاذاكشي ديال فيلترز و فورما ماكاينش غير في docker ps، كاين حتى بالنسبة لimages.<br>
    كاين شي اختلافات و لكن قليلة، و هذا واحد منها <br>
    ال dangling images هو واحد النوع في شكل images لي غالبا غادي تكون فايت شايفهم (هاذوك لي سميتهم None و لي شادين ليسباص بلا سبب) .<br>
    الfilter-- ديال docker images تاتعطينا الامكانية أننا نجبدو هاذ الimages
</div>

<div dir="rtl"><ul>
    <li>ايلا بغيتي تمسح جميع dangling image و تخوي شوية السطوكاج</li>
</ul></div>

    $ docker rmi -f $(docker images -qf "dangling=true")

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>ماشي جميع images لي سميتهم none تايكونو dangling و تايكونوا بدون فائدة .</li>
        <li>منين تاتدير build أو pull لشي image عندك أصلا و بنفس tag . تايمشي docker يحيد للقديمة tag باش يطاكّي الجديدة، وهنا فين تايخرجو dangling images</li>
    </ul>   
</div>