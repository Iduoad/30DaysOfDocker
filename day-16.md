# 30 Days of Docker - Day 16

<div dir="rtl">
    اليوم غادي نهضرو على واحد command مامشهوراش بزااف و لكن مهمة بزاف خاصة في debugging و في long running containers ..<br>
    الكومند هي docker diff .. هاذ الكوموند تاترد لينا التغييرات لي طراو في container ديالنا منين تcrea'ya ..
</div>

    docker exec -it DevC bash
    touch /app/docker.md
    rm /app/text.txt
    cat "hello" >> /app/devc.txt
    # Results
    C /app
    A /app/docker.md
    D /app/text.txt
    C /app/devc.txt

<div dir="rtl">
    كيفما تانشوفو الoutput تايكون على شكل file path و حداهم على اليمين إما C (Changed) أو A)added) أو D)Deleted)
</div>