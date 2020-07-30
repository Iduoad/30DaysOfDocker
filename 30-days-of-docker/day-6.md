# 30 Days of Docker - Day 6

<div dir="rtl">
    غادي ناخدوا استراحة من commands و نهضروا على كيفاش containers يقدروا يسهلوا علينا شي حوايج لي ممكن يكونوا شوية معنكشين .<br>
    مثلا ايلا بغيتي تدوز requests ديالك من Tor Network و تحس براسك آنونيموس بكل سهولة 😁 ، ممكن تدير هاذشي بكل بساطة باستعمال واحد community image سميتها <a href="https://hub.docker.com/r/dperson/torproxy">dperson/torproxy</a> لي مقادة باش تدير هاذشي
</div>

<div dir="rtl"><ul>
    <li>أولا جبد public ip address ديالك </li>
</ul></div>

    $ curl ifconfig.me

<div dir="rtl"><ul>
    <li>من بعد صايب كونتينر ديال torproxy</li>
</ul></div>

    $ sudo docker run -it -p 8118:8118 -p 9050:9050 -d dperson/torproxy

<div dir="rtl"><ul>
    <li>عاود جبد public ip address ديالك، ولكن هاذ المرة مور البروكسي .. تاداااا 🎉</li>
</ul></div>

    $ curl -x 127.0.0.1:8118 ifconfig.me