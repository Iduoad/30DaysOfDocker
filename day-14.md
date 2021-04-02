# 30 Days of Docker - Day 11

<div dir="rtl">
   البوسط لي داز كان على shell scripting و شي حوايج لي ممكن ينفعونا نكتبوا Dockerfiles ديالنا .. هاذ البوسط غادي يكون كمالة على ذاكشي لي كنا بدينا .. 
</div>

<div dir="rtl"><ul>
    اليوم غادي نهضرو على Filename Expansion و Docker و واحد الحاجة مهمة لي كاتستعمل بزاف في dockerfiles و ماهضرناش عليها المرة لي دازت و لي هي shopt -s nullglob
</ul></div>

<div dir="rtl"><ul>
    الposix shells فيهم واحد الخاصية سميتها Filename Expansion و هي منين تانعطيوه شي filename و تانعطيوه وسط منو واحد من [ ] أو * أو ? تاحاول يستعملهم باش يجبد filenames كاميلين مثلا
</ul></div>

    # this will delete all pdf file in the working directory 
    rm *.pdf
    # This will remove mp3, mp4 and any files ending with "mp" followed by a character
    rm *.mp?
    # this will remove all files starting with a, n or k
    rm [akn]*

<div dir="rtl">
    في حالة ايلا shell ماقدرش يدير expansion تايدوز هاذيك glob كيفما هي للcommand و هاذشي لي تايعطينا error على حساب command لي استعملنا.<br>
    اش نفهموا أكثر آجي نتخيلو واحد function تانعطيوها واحد المجموعة ديال files و هي تاتدير عليهم شي خدمة.<br>
    المشكل ايلا دوزنا ليها شي glob لي ماتاتماتشي والو غادي يدوزها هاكاك و هاذشي يقدر يعطينا شي حاجات ماشي هي هاذيك.<br>
    باش نحلو هاذ المشكل انستعملو nullglob لي في حالة الglob ماماتشات والو تاترد لينا empty string ""
</div>


    # if we execute this statement
    myfunction *.pdf
    ## if there are pdf files in cwd the shell will execute this
    ## > myfuction 1.pdf 2.pdf book.pdf
    ## if there are no pdf files
    ## > myfunction "*.pdf"
    ## Since there is no file named "*.pdf" our function will file (a lot of times silently)
    ## if nullglob is on
    ## > myfunction ""

<div dir="rtl">
    ممكن نستعملو failglob لي تاتحبس الscript ايلا كان شي مشكل و لكن عموما هاذا هو التصرف الاعتيادي ايلا كنا خدامين ب set -e
</div>