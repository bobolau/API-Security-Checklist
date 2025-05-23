[English](./README.md) | [繁中版](./README-tw.md) | [简中版](./README-zh.md) | [العربية](./README-ar.md) | [Azərbaycan](./README-az.md) | [Български](./README-bg.md) | [বাংলা](./README-bn.md) | [Català](./README-ca.md) | [Čeština](./README-cs.md) | [Deutsch](./README-de.md) | [Ελληνικά](./README-el.md) | [Español](./README-es.md) | [فارسی](./README-fa.md) | [Français](./README-fr.md) | [हिंदी](./README-hi.md) | [Indonesia](./README-id.md) | [Italiano](./README-it.md) | [日本語](./README-ja.md) | [한국어](./README-ko.md) | [ພາສາລາວ](./README-lo.md) | [Македонски](./README-mk.md) | [മലയാളം](./README-ml.md) | [Nederlands](./README-nl.md) | [Polski](./README-pl.md) | [Português (Brasil)](./README-pt_BR.md) | [Русский](./README-ru.md) | [ไทย](./README-th.md) | [Türkçe](./README-tr.md) | [Українська](./README-uk.md) | [Tiếng Việt](./README-vi.md)

# API Аюулгүйн жагсаалт

API гаргах, загварчлах, тестлэхэд аюулгүйн талаас авах сөрөг арга хэмжээний жагсаалт.

---

## Authentication

- [ ] `Basic Auth` бүү ашигла, Стандарт authentication ашигла (Жнь. [JWT](https://jwt.io/), [OAuth](https://oauth.net/)).
- [ ] `Authentication` -ын `token generation`, `password storage` зэргийг бүү дахин шинээр хий, стандарт ашигла.
- [ ] Нэвтрэх(Login) үед `Max Retry` ашиглан хорилт хий.
- [ ] Чухал өгөгдлүүдийг encrupt хий.

### JWT (JSON Web Token)

- [ ] Санамсаргүй үүссэн түлхүүр (`JWT Secret`) ашиглаж token -ыг brute force -оос хамгаал.
- [ ] Payload -аас алгоритмаа бүү задал. Backend дээрээ хий (`HS256` эсвэл `RS256`).
- [ ] Токен дуусах хугацаа (`TTL`, `RTTL`) аль болох бага болго.
- [ ] Чухал өгөгдлийг JWT payload -д бүү хадгал, decode хийхэд [амархан](https://jwt.io/#debugger-io).
- [ ] Хэт их мэдээлэл хадгалахаас зайлсхий. JWT нь ихэвчлэн headers хэсэгт хуваагддаг бөгөөд тэдгээр нь хэмжээ хязгаартай байдаг.

## Access

- [ ] Хүсэлтийн тоог хязгаарлаж (Throttling) DDoS / brute-force дайралтаас хамгаална.
- [ ] HTTPS ашиглаж сервер талдаа MITM (Man In The Middle Attack) дайралтаас хамгаална.
- [ ] `HSTS` header -ыг SSL дээр ашиглаж SSL Strip дайралтаас хамгаална.
- [ ] Лавлах жагсаалтыг унтраа.
- [ ] Хувийн API-уудын хувьд зөвхөн зөвшөөрөгдсөн жагсаалтад орсон IP/хостоос хандахыг зөвшөөрнө үү.

## Authorization

### OAuth

- [ ] `redirect_uri` -ыг үргэлж сервер талд шалган зөвшөөрөгдсөн URL эсэхийг шалга.
- [ ] Аль болох токен биш код солилц (`response_type=token` -ыг зөвшөөрч болохгүй).
- [ ] OAuth authentication -ын үед `state` параметрийг санамсаргүй үүссэн hash ашиглан CSRF ээс сэргийлнэ.
- [ ] Хувьсагчид анхны утга заавал оноож өг, утгыг байнга шалга.

## Input

- [ ] Яг зөв HTTP хүсэлтийг ашигла: `GET (унших)`, `POST (үүсгэх)`, `PUT/PATCH (орлуулах/солих)`, мөн `DELETE (устгах)`, бас `405 Method Not Allowed` -ыг хүсэлтийн төрөл тодорхойгүй үед ашигла.
- [ ] `content-type` -ыг хүсэлтийн header (Content Negotiation) дээр шалгаж зөвхөн дэмжигдсэн төрлийг зөвшөөр (Жнь. `application/xml`, `application/json`, гэх мэт) бас төрөл нь таарахгүй бол `406 Not Acceptable` хариу буцаа.
- [ ] `content-type` -ыг post хийх өгөгдөл дээр шалга (Жнь. `application/x-www-form-urlencoded`, `multipart/form-data`, `application/json`, г.м).
- [ ] Хэрэглэгчээс гараас оруулсан утгыг шалгаж түгээмэл нүхнүүдээс сэргийлнэ. (Жнь. `XSS`, `SQL-Injection`, `Remote Code Execution`, г.м).
- [ ] Чухал өгөгдлүүдийг (`credentials`, `Passwords`, `security tokens`, эсвэл `API keys`) URL ээр бүү явуул, оронд нь стандарт Authorization header ашигла.
- [ ] Зөвхөн сервер талын шифрлэлтийг ашиглана уу.
- [ ] API Gateway үйлчилгээ ашиглан Rate Limit Policies (Жнь. `Quota`, `Spike Arrest`, `Concurrent Rate Limit`) болон cache хийх, мөн API deploy хийхэд ашигла.

## Processing

- [ ] Нэвтрэх явцад алдаа гарахаас сэргийлж бүх endpoint -уудыг нэвтрэх шаардлагатай эсэхийг шалгах.
- [ ] Хэрэглэгчийн ID ашиглахаас зайлсхийх. `/user/654321/orders` үүний оронд `/me/orders` ашиглах.
- [ ] Автоматаар нэмэгдэх ID бүү ашигла. `UUID` ашигла.
- [ ] XML файл parse хийх үед entity parse бүү хий ингэснээр `XXE` (XML external entity attack) -аас сэргийлнэ.
- [ ] XML файл parse хийх үед entity expansion бүү хий ингэснэр `Billion Laughs/XML bomb` дайралтаас сэргийлнэ.
- [ ] Файл upload хийхэд CDN ашигла.
- [ ] Их хэмжээний өгөгдөлтэй ажиллах үед Workers болон Queue ашиглан үйлдлийг аль болох background -д ажиллуулж хариуг хурдан явуулах нь HTTP Blocking -оос сэргийлнэ.
- [ ] DEBUG горимыг унтраах.
- [ ] Боломжтой үед гүйцэтгэх боломжгүй stack ашигла.

## Output

- [ ] `X-Content-Type-Options: nosniff` header дээр явуул.
- [ ] `X-Frame-Options: deny` header дээр явуул.
- [ ] `Content-Security-Policy: default-src 'none'` header дээр явуул.
- [ ] Ул мөр үлдээх `X-Powered-By`, `Server`, `X-AspNet-Version` header үүдыг устга.
- [ ] `content-type` -ыг хүсэлтийн хариуд нь харгалзан буцаах, Хэрвээ `application/json` хүсэлт явсан бол хариуд нь `content-type` нь `application/json` байх.
- [ ] Чухал өгөгдлүүд `credentials`, `Passwords`, `security tokens` бүү буцаа.
- [ ] Тухайн ажилд тохирсон статус код илгээх. (Жнь. `200 OK`, `400 Bad Request`, `401 Unauthorized`, `405 Method Not Allowed`, г.м).

## CI & CD

- [ ] unit/integration тест ашиглан системийн загварчлал, хэрэгжилтийг шалгах.
- [ ] Код шалгалт ашигла, мөн өөрөө өөрийгөө ч шалга.
- [ ] Бүх тусдаа хэсгүүд бүр vendor сан, бусад нэмэлт сангууд бүгдийг нь AV програмаар статикаар шалга.
- [ ] Код дээрээ аюулгүй байдлын тестийг (статик/динамик анализ) тасралтгүй ажиллуул.
- [ ] Мэдэгдэж буй сул талуудыг өөрийн хамаарлыг (програм хангамж болон үйлдлийн систем) шалгана уу.
- [ ] Ямар ч үед deploy хийхэд амар шийдэл гаргах.

## Monitoring

- [ ] Use centralized logins for all services and components.
- [ ] Use agents to monitor all traffic, errors, requests, and responses.
- [ ] Use alerts for SMS, Slack, Email, Telegram, Kibana, Cloudwatch, etc.
- [ ] Ensure that you aren't logging any sensitive data like credit cards, passwords, PINs, etc.
- [ ] Use an IDS and/or IPS system to monitor your API requests and instances.

---

## Мөн үзнэ үү:

- [yosriady/api-development-tools](https://github.com/yosriady/api-development-tools) - RESTful HTTP+JSON API-г бүтээхэд хэрэгтэй нөөцүүдийн цуглуулга.

---

# Оролцоо

Энэ рэпод оролцох бол fork хийж өөрчлөлтөө оруулаад pull request үүсгэнэ үү. Асуулт байвал бидэнтэй холбогдоорой `team@shieldfy.io`.
