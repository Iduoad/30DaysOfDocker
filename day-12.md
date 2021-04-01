# 30 Days of Docker - Day 12

<div dir="rtl">
   اليوم غادي نكملو على نفس الأفكار ديال الايام ليدازو و غادي نهضرو على واحد القاعدة مهمة ديال Docker لي هي One Process per container ..<br>
   واخا تاتبان بسيطة، هاذ القاعدة ضروري نكونوا فاهمينها باش نطيحوش في مشاكل من بعد ..
</div>

<div dir="rtl">
    بما أن Docker is a process container system يعني أنه تايهمتم بprocess واحد و تاrun'eh بواحد الطريقة لي تاتخليه معزول على البقية ديال processes عكس Machine container systems بحال LXC مثلا لي مديوريين باش يتكلفو بuse cases فين ماينين Processes بزاف..
</div>

<div dir="rtl">
    أهم حاجة هنا هي process واحد .. docker دائما تايفترض أنه مخدم غير process واحد هو لي تايكون في CMD أو ENTRYPOINT (لي شفناهم المرة لي فاتت) و لي تايكون عندو PID1 ..
</div>

<div dir="rtl">
    من بعد Docker تايبقى على تواصل مع هاذ الprocess دائما باستعمال IPC signals لي باستعمالهم تايعرف واش باقي حي و ليبيهم تايقتلو ايلا بغا .. <br>
    هاذ المبدأ يقدر يبان لينا بايخ و ماشي مهم، و لكن مهم بزاف ..
</div>

<div dir="rtl">
    نفترض أننا في ENTRYPOINT تانطلبو من Docker يخدم لينا واحد Shell script لي براسو تايخدم بزاف ديال programs مثلا nginx و php-fpm و شي php scripts لي تايديرو شي حاجة ..
</div>

    #!/bin/bash
    nginx & 
    php-fpm &
    php ./debugging.php &
    php ./observability.php &
    ---
    # Dockerfile
    ENTRYPOINT ["script.sh"]t

<div dir="rtl">
    في الحالة العادية، ايلا مات شي واحد من هاذ الprograms غادي نبغيو docker يعرف، و ياخد القرار ولا يسيفط المعلومة لشي بلاصة (لkubernetes مثلا) .. و لكن ماشي هاذشي لي غادي يوقع حيت docker ما عندو تاشي علاقة بهاذ الprograms و تايعرف غير مول PID1 لي هو shell ديالنا bash أو sh
</div>

    docker exec -it devC bash
    pkill nginx 

    # Nothing will happen, 
    # the container will still be up an running

    kill 1 # which will kill /bin/bash
    # This will code the container to exit

<div dir="rtl">
    في هاذ الحالة الحل هو نطوروا ذاك الscript ديالنا باش يتكلف ب Error handling و يصيفط signals لDocker ما ان طرى شي حاجة لشي process أو نستعملو شي program لي متخصص في process management بحالsupervisor أو dumb-init
</div>