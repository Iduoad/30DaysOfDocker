# 30 Days of Docker - Day 26
المرة لي فاتت هضرنا على docker daemon و كيفاش ممكن نستعملوا docker cli باش نهضروا معاه فينما كان باستعمال TCP أو باستعمال Unix Sockets مع SSH أو بلا SSH

دابا آجي نتخيلوا عندنا بزاف ديال Docker daemons في بزاف دالبلايص، مثلا واحد في الحاسوب ديالنا، وواحد في الريزو ديال الخدمة مExposer في ماشين سميتها devc.local في البورت 10000 و واحد في أنترنت devc.com و لي ممكن نهضروا معاه غير بSSH 

كيفاش ممكن نهضروا مع هاذشي كامل بسهولة ؟
هنا فين تايجي الدور ديال Docker contexts .. ممكن تصايبوا context لكل واحد من هاذز لي هدرنا عليهم و نبقاو نسويتشيو بيناتهم بسهولة.