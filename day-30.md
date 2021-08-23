# 30 Days of Docker - Day 11

<div dir="rtl">
   اليوم غادي نهضروا على CMD و ENTRYPOINT .. هاذ الموضوع فلسفي و أزلي في Docker و متلف العالم كامل و منهم أنا ..<br>
   عموما منين تانbuild'ew شي container image تانكونوا أمام 2 ديال الخيارات ..
</div>

<div dir="rtl"><ul>
    <li>الاول هو أن الimage تاتكون عبارة عن package للآبليكاسيون ديالنا .. يعني تانوجدو كّاع ذاكشي لي خاص الآبليكاسيون باش تخدم في runtime و تانقولو لDocker أنها Runnable و كيفاش غادي يrunيها.<br>
    هنا تانستعملوا Docker من اجل Packaging يعني في آخر المطاف هاذيك Image غادي هي الطريقة الكافية باش أي واحد يخدم الأبليكاسيون ديالنا (Process)<br>
    في هاذ الحالة كايخاصنا نقولو لDocker منين يجي image ديالنا، يعني شناهو الProcess لي تايشكل الهوية ديال أبليكاسيون ديالنا. و هذا هو entrypoint ديال image ديالنا.<br>
    هاذا هو الusecase الأكثر شيوعا ديال docker و images في هاذ السياق هوما images ديال أبليكاسيونات ديالنا لي تانصايبو.
    </li>
</ul></div>

<div dir="rtl"><ul>
    <li>الخيار الثاني هو تانستعملو docker باش نصايبو واحد الوسط مناسب (يعني فيه libs و dependencies لي بغينا) فين نrun'ew شي commands و شي Applications ديالنا.<br>
    هنا كانهضرو على images بحال ديال gnu/linux distro ولا ديال programming ecosystems بحال python أو node.js ....<br>
    في هاذ الحالة image ديالنا ماتاتكونش مراد منها تكون package و لكن تاتكون ecosystem .. و هاذشي لي تايخليها ماتايكونش عندها Entrypoint واحد مفروض على user في runtime .. و لكن بالعكس تايكون مطلوب منها تكون قادرة تexecute واحد العدد ديال commands aka CMD <br>
    في هاذ الUsecase تايكون ممكن لينا نحددوا CMD في الBuild و لكن ماتاتكونش مفروضة علينا في الRun و تايمكن لينا نبدلوها بسهولة<br>
    دابا من بعد ما هضرنا على ENTRYPOINT و CMD و الفرق بيناتهم و Motivation ديال كل واحدة .. آجي نشوفو كيفاش نخدموهم.<br>
    عمليا، ENTRYPOINT و CMD عندهم نفس المفعول في أغلب الحالات.. الفرق هو أن CMD ممكن تبدلوها بcommand لي بغينا في Runtime
    </li>
</ul></div>

    # dockerfile
    ...
    ENTRYPOINT ["node", "devc.rabat.js"]
    ...
    # ---

    # this will run the devc rabat node application.
    docker run -it devc:rabat

<div dir="rtl">
    نفس المثال بCMD
</div>

    # dockerfile
    ...
    CMD ["node", "devc.rabat.js"]
    ...
    # ---

    # this will run the devc rabat node application.
    docker run -it devc:rabat 
    # but this will run the devc casa node application.
    docker run -it node devc.casa.js

<div dir="rtl">
    واحد من usecases الزوينين لCMD هو نستعملوها باش ندوزو Parameters لENTRYPOINT ديالنا مادام المحتوى ديال CMD دائما تايتزاد في الأخير (هاذ اللعيبة تاتخدم في Exec form فقط) 
</div>

    # dockerfile
    ...
    CMD ["--help"]
    ENTRYPOINT ["node", "devc.js"]
    ...
    # ---

    # this will display the help message for our app
    docker run -it devc:rabat
    # this will run our app with awesome argument.
    docker run -it devc:rabat awesome

---
<div dir="rtl">ملاحظات:
    <ul>
        <li>حتى ENTRYPOINT ممكن نبدلوه في Runtime باستعمال entrypoint-- و لكن غير منصوح بيها حيث غانكون تانبدلو الهوية ديال container بحد ذاتها</li>
        <li>كنت بغيت نهضر على One process per container Philosophy و كيفاش تاتأثر في Design ديال Dockerfiles و CMD و ENTRYPOINT و لكن تايبان لي غادي نخليوها لمرة أخرى</li>
    </ul>   
</div>