# 30 Days of Docker - Day 27

<div dir="rtl">
  
من الحوايج لي ممكن نستعملوا docker فيهم هو تخدموا stacks ديالنا، (يعني أبليكاسيون بكلشي ليها) و هاذشي ممكن نديروه بسهولة باستعمال docker compose .

من الحوايج لي صعيب نديرهم بdocker compose هو batch computing يعني بزاف ديال الحوايج لي غادي نرانيوهم بواحد الترتيب و ربما غادي يكونوا مرتبطين ببعضهم. 
في الحالات الصعابين ممكن نستعملوا شي tool معين بحال Kubernetes  و لكن في أغلب الحالات، سكريبت كافي.

من الحوايج لي ممكن ينفعونا في هاذ القضية بزاف هي docker wait لي كاتتسنى واحد الcontainer حتى تايسالي و تاتكتب exit status ديالو
مثال في الكود ممكن تستعمل هاذ البلان باش تدير CI/CD ديالك راسك 🤪
  
</div>

```bash
# Download music from internet
jobl=$(docker run -d --rm -v /home/devc/Music:/Music devc-music-downloader:latest) 
exit_code=$(docker wait $jobl) 
test $exit_code -eq 11 || exit $exit_code

# convert it using ffmpeg 
job2=$(docker run -d --rm -v /home/devc/Music:/Music -v ./transcode.sh:/transcode sh linuxserver/ffmpeg <devc-ffmpeg-command>) 
exit_code=$(docker wait $job2) 
test $exit_code -eq 11 || exit $exit_code 

# Upload it to s3 bucket 
job3=$(docker run -d --rm -v /home/devc/Music:/Music devc-s3-uploader:latest) 
exit_code=$(docker wait $job3) 
test $exit_code -eq 11 || exit $exit_code 

# Notify Music Server to sync new music from S3 
job4=$(docker run -d --rm devc-mediaserver-notifier:latest) 
exit_code=$(docker wait $job4) 
test $exit_code -eq 11 || exit $exit_code 

```