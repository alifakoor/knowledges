لینک ویدئو:
https://www.youtube.com/watch?v=j5hRuZY7V9w

نکات:
pulumi - infrastructure as code
could sandboxing - developed by divar - for resolve dependencies when a developer want to test their changes
telepresence - https://github.com/telepresenceio/telepresence
kuber helm - package manager
rpc framework - 
service mesh

کدریویو زیر ۲۴ ساعت باید انجام شود
با داکیومنت‌ها چک می‌شود
از linter استفاده کنید static analysis
A/B test
زیرساخت برای A/B test
برای اینکه این داستان تست و آزمایش به صورت محصولی و فنی انجام بشه:
divar experiment - for test and experience
مقاله: overlaping experiment infrastructure: more, better, faster experimentation
experiment orthogonal


https://martinfowler.com/ => feature toggles
spotify => feature trains

SLO, performance metrics

AUTOMATION

development platform team
sre platform team
https://sre.google/

on call primary, secondary

هرچی automation بهتر باشه on call کارش راحتتره

بعد از ریلیز باید یه سری متریک و لاگ باشند که بهم بگن الان این نسخه من خوبه یا بد
این متریک، متریک رم و cpu هم نیست، متریک از دید کاربر هستند: latency, availability, throughput, saturation
 latency: زمان api چقدر بود
 availability: چندتا از apiها اوکی هستند چندتاشون خطا میدن؟ 

prometheus, thanos

tracing, time series (victoria metrics)
مانیتورینگ خیلی مهمه

تغییر یک شبه و یک شکل نیست، من نمیتونم برم بگم اگر چهارتا شرکت از کوبر استفاده میکنن منم باید استفاده کنم

kent beck https://www.kentbeck.com/


engineering productivity
developer productivity
developer experience
engineering productivity and efficiency
کار این تیم‌ها اینکه بار ذهنی رو (در یک شرکت متوسط به بالا) از ذهن توسعه‌دهنده‌ها بردارند، یعنی من اگر یه ci/cd خوب بدم، توسعه دهنده دیگه لازم نیست بره خودش همچین سیستمی پیاده کنه


https://changebyattraction.simplecast.com/
