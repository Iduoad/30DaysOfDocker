# 30 Days of Docker - Day 23

<div dir="rtl">
اليوم غادي نهضروا على شوية ديال المفاهيم Terminology لي عندها علاقة ب container images .. هاذ المفاهيم غادي ينفعونا في البوسطات الجايين.
المفاهيم هي:

### الContainer Image :

هي واحد المجموعة ديال الملفات غالبا tar files لي مرتبين على شكل طبقات layers. كل طبقة تاتخزن التغيير في Filesystem لي تدار مقارنة بالطبقة لي قبل منها. هاذ التغييرات تايتدارو في أغلبية دالحالات بفعل الكومندس لي في Dockerfile ديالنا و تايتسماو بلغة containers ب Image Filesystem Changeset أو Image Diff
مثلا ايلا عندنا في الDockerfile

```
RUN touch DevC.md
```

المحتوى ديال Changeset غادي يكون هاذاك DevC.md لي زدنا.

### ال Container registry

هي واحد البلاصة في ممكن نخزنوا الimages ديالنا بطريقة فعالة و optimized .. من registry المعروفين هوما Docker hub و Quay و Gitlab registry و gcr و ecr و غيرهم

### ال image repository و image tag 

منين تانبغيو نbuildiw شي image تايخاصنا نحددو 2 ديال الأجزاء من بعد ديك t- الجزء الأول ديال الrepository و الثاني الtag ..
الrepository ممكن يكونوا فيه بزاف ديال images بtags مختلفين. مثلا

```
  php:fpm-buster
  php:apache
  php:7.3-alpine
```
  
الrepository هو php و الجزء لي من بعد تايتسمى tag و تايحدد image مختلفة. منين غادي نpush'ewهم كاملين في شي container registry غادي يكونوا تاينتاميو لنفس repository

</div>
