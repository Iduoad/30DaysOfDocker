# 30 Days of Docker - Day 26

<div dir="rtl">

المرة لي فاتت هضرنا على docker daemon و كيفاش ممكن نستعملوا docker cli باش نهضروا معاه فينما كان باستعمال TCP أو باستعمال Unix Sockets مع SSH أو بلا SSH

دابا آجي نتخيلوا عندنا بزاف ديال Docker daemons في بزاف دالبلايص، مثلا واحد في الحاسوب ديالنا، وواحد في الريزو ديال الخدمة مExposer في ماشين سميتها devc.local في البورت 10000 و واحد في أنترنت devc.com و لي ممكن نهضروا معاه غير بSSH 

كيفاش ممكن نهضروا مع هاذشي كامل بسهولة ؟
هنا فين تايجي الدور ديال Docker contexts .. ممكن تصايبوا context لكل واحد من هاذز لي هدرنا عليهم و نبقاو نسويتشيو بيناتهم بسهولة.

```bash
# Create docker contexts 
docker context create --docker host=unix:///var/run/docker.sock mine 
docker context create --docker host=tcp://devc.local:10000 devc-local 
docker context create --docker host=ssh://devcuser@devc.com devc-com

# List all contexts 
docker context list 

# Switch to our local one
docker context use mine 
## Execute commands against my docker daemon
docker ps 
docker run devc:latest 

# Switch to DevC local context
docker context use devc-local 
## Execute commands in DevC local daemon via TCP 
docker ps 
docker run devc:latest 

# Switch to devc-com context
docker context use devc-com 
## Execute commands in the devc-com host via ssh. 
docker ps docker 
run devc:latest 
```

</div>
