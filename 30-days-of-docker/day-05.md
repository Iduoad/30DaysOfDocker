# 30 Days of Docker - Day 5

<div dir="rtl">
    شفنا قبل كيفاش نجبدوا المعلومات باستعمال docker ps و docker images عاوتاني .. اليوم غادي نشوفوا طريقة أقوى باش نجبدوا معلومات أكثر على containers و images لي هي docker inspect لي كاتعطي جميع المعلومات تقريبا .<br>
    لي زوين في docker inspect هي أنها by default تاتعطي النتيجة على شكل json لي ممكن تبارسيه Parse و تجبد لي بغيتي .
</div>

<div dir="rtl"><ul>
    <li>باش نجبدوا المعلومات على image ديالنا DevC:rabat و تخبيهم في json file</li>
</ul></div>

    $ docker inspect --type image DevC:rabat > DevC.json

<div dir="rtl"><ul>
    <li>باش نجبدوا معلومات علىnetworking ديال container ديالنا و نديروه في الرابور لي غانصيفطو لSRE باش يشوف شنو المشكل</li>
</ul></div>

    $ echo -e "\`\`\`json\n$(docker inspect devC | jq '.[0].NetworkSettings')\n\`\`\`" > report.md

<div dir="rtl"><ul>
    <li>    باش نحضيو capabilities ديال containers .. و نكتبوا شي حاجة ايلا شي حاجة ماشي هي هاذيك</li>
</ul></div>

    $ docker inspect 86e2d8181c53 | jq -r '.[0].EffectiveCaps' | grep -i DAC_OVERRIDE > /dev/null && echo "Fin awa ghaadi ?"
---
<div dir="rtl">ملاحظات:
    <ul>
        <li>بالنسبة type-- تاتنفع منين تايكون عندك container و image بنفس الاسم.</li>
        <li>بالنسبة للبارسين parsing ممكن تديرو بلغة البرمجة ديالك أو بjq لي هو CLI tool ساهل و سريع 😃 </li>
        <li>النتيجة ديال docker inspect تاتكون على شكل array </li>
    </ul>   
</div>