# 30 Days of Docker - Day 25

<div dir="rtl">

اليوم غادي نهضروا على واحد البلان زوين بزاف و مفيد، و لي غادي يقدر ينفع بزاف ديال الناس، خاصة الناس لي خدامين Docker في CI/CD
في Docker عندنا بزاف ديال المكونات منهم Docker Daemon لي هو لي تانهضروا معاه بDocker CLI أو Docker-compose باش يقضي لينا الغرض.

التواصل مع هاذ الDocker Daemon تايتدار إما عن طريق Unix Socket لي هو فيشيي تانطتبوا فيه باش نهضروا مع Docker أو عن طريق TCP لي هو port تانهضروا فيه مع Docker
واخا ال Unix Socket هو default في Docker تايبقى Limited حيت مايمكنش نهضروا مع Docker daemon إلا ايلا كان في نفس الحاسوب. ذاكشي علاش TCP بلان زوين.

```bash
#### Dockerd #### 
# start docker daemon (listen to Unix socket) 
sudo dockerd -H unix:///var/run/devc.sock 

# start docker daemon (listen to default port on 2 interfaces) 
sudo dockerd -H tcp://192.168.59.106 -H tcp://10.10.10.2 

# start docker daemon (listen to 9999 tcp port on all tnterfaces) 
sudo dockerd -H tcp://0.0.0.0:9999 



### Docker CLI #### 
# List all running containers on first docker host (daemon) 
sudo docker -H unix:///var/run/devc.sock ps 

# Run DevC container on the second docker host (equivalent) 
sudo docker -H tcp://192.168.59.106 run -it devc:latest sudo docker -H tcp://10.10.10.2 run -it devc:latest 
```

و لكن TCP تايجي بمشاكلوا تا هو حيت غادي يخلي Docker daemon ديالنا محلول للناس لي معانا في الريزو، و غادي يخاصنا نأمنوه و نسيكيريزيوه باش مانتصيدوش.
   
كاين واحد الحل وسط: Docker تايعطينا الإمكانية أننا نتكونيكطاو لDocker daemon عن بعد باستعمال SSH و ندوزو الكوموند ديالنا عبر SSH النيت بلا مانحتاجوا نExposew الDaemon
.

```bash
#### Docker using SSH #### 
# List running containers on the devc docker host via SSH 
# This requires SSH access only (docker daemon is not exposed to the outside world) 
sudo docker -H ssh://devc-user@devc.com ps 

# We can use DOCKER_HOST env variable to specify the docker host 
# When specifying DOCKER_HOST we can ommit the -H directive 
export DOCKER_HOST=ssh://devc-user@devc.local 
# These commands will be run on the remote machine devc.local 
sudo docker run -d devc:latest 
sudo docker-compose -f devc-stack.yml up 
```

</div>
