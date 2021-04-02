# 30 Days of Docker - Day 15

<div dir="rtl">
    هذا غادي يكون آخر بوسط على shell scripting <br>
    في الأول كنت بغيت ندير بوسط على expansions و لكن لقيت بلي غادي يخاص بزاف ديال الكتابة داكشي علاش غادي نحاول نهضر اليوم على substring expansion فقط لي مفيدة بزاف ..

</div>

<div dir="rtl">
    قبل مانعرف substring expansion فينما كنت تانبغي نخدم على شي حاجة لي تاتحتاج بزاف ديال string manipulation تانفكل مباشرة في python (أي high level scripting language قاضي الغرض) .. و لكن دابا وليتا تانخدم غير بBash صافي.. <br>
    الsyntax ساهلة {param:offset:limit}$ <br>
    بحيث أن param هي variable ديالنا (shell parameters مفهموم أشمل في shells تايضم حتى الvariables) و الoffset هو منين بغينا نبداو slice و limit هو عدد الcharacter لي بغينا ناخدو ..
</div>

    a="DevC Rabat"
    echo ${a} # basic param expansion
    echo ${a:5} # >> Rabat
    echo ${a:0:4} # >> DevC
    echo "${a:5} ${a:0:4}" >> Rabat DevC

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>هاذ القضية تاتنفع بزاف في scripts ديالنا ولكن المشكل ديالها هو أنها ماشي POSIX يعني ماكايناش في sh و هاذشي علاش خاص نردو معاها البال في Dockerfiles و ENTRYPOINT و نسبقوها ب bash -c أو نزيدو Shebang الفوق فيها bash ايلا كان سكريبت ..</li>
    </ul>   
</div>