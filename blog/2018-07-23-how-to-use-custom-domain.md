---
title:  چطور از دامنه شخصی خود برای سرویس فندق استفاده کنیم؟
author: سکوی ابری فندق
author_image_url: /img/fandogh.png
tags: [fandogh_paas, docker, paas, service, domain]
image: /img/blog/fandogh-paas-banner.svg
---

![Custom Domain](/img/blog/custom-domain.svg 'Custom Domain')

 مواردی وجود دارد که کاربران نیاز دارند تا برای سرویس های خود روی فندق از دامنه دلخواهی مثل
`api.my-domain.com`
استفاده کنند.این کار به سادگی توسط fandogh-CLI امکان پذیر است، ابتدا باید دامنه را ثبت و مالکیت خود را اثبات کنید سپس می‌توانید سرویس را روی دامنه مورد نظر deploy کنید.

<!--truncate-->

## ثبت دامنه جدید در فندق

ابتدا در CLI ‌لاگین کنید سپس دستور زیر را اجرا کنید:

```bash
$ fandogh domain add --name api.my-domain.com
```

با اجرای این دستور دامنه مورد نظر در اکانت شما  ثبت می‌شود و یک Key ‌نمایش داده می‌شود. برای اینکه مالکیت خود را روی دامنه اثبات کنید لازم است یک TXT رکورد روی دامنه  `api.my-domain.com` ایجاد کنید و مقدار Key ای که از CLI دریافت کردید را در آنجا قرار دهید.<br/><br/>
اگر TXT record ‌به درستی تنظیم شده باشد دامنه شما تایید می‌شود و به اکانت فندق شما اضافه می‌شود.

## deploy سرویس روی دامنه مورد نظر

deploy سرویس روی دامنه مورد نظر مثل deploy هر سرویس دیگری است تنها کافیست از سوئیچ `host—-` استفاده کنید:

```bash
fandogh service deploy --hosts api.my-domain.com
```

به این ترتیب اگر دامنه به درستی ثبت و تایید شده باشد سرویس شما deploy می‌شود و روی آدرس مورد نظر قابل دسترس است.

## تنظیم کردن CNAME

توجه داشته باشید که باید روی DNS Server دامنه مورد نظر یک CNAME  به آدرس فندق سرویس خود ایجاد کنید.
برای این کار لازم است یک رکورد [CNAME] [cname] با نام `lb.fandogh.cloud` بر روی دامنه خود ایجاد کنید.

[cname]: https://en.wikipedia.org/wiki/CNAME_record
