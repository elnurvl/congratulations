# Congratulations
Sizə Facebookda təbrik mesajı yazan şəxslərin siyahısı lazımdır?
Özünüzün tək-tək bu şəxslərin adını seçməyə vaxtınız yoxdur?

Elə isə [Təbriklər](https://tebrikler.tk) tətbiqindən istifadə edin!

Bir kliklə sizə təbrik mesajları yazmış şəxslərin siyahısını əldə edin: beləcə siz insanlara diqqətinizi bildirmək üçün əldə etdiyiniz siyahını növbəti paylaşacağınız statusda qeyd edə bilərsiniz.

## Hacker mode
Ad siyahısını sadəcə təbrik sözlərinə görə yox, həmçinin öz kriteriyanıza görə də çıxara bilərsiniz. Bunun üçün "hacker mode"u yandırıb söz siyahısını kontekstə uyğun olaraq dəyişməniz kifayətdir: bildirdiyiniz tarix aralıqlarında sizə qarşı bu sözləri işlədən şəxslərin siyahısı qarşınızda olacaq.

**Nümunə 1**

Siz son 2 il ərzində sizə sevgi mesajları yazanların adlarını öyrənmək istəyirsiniz.

1. "Hacker mode"u yandırırsınız.
2. Tarix aralığını son 2 ili əhatələyəcək şəkildə seçirsiniz.
3. Söz siyahısında təbrik sözlərini sevgi sözləri ilə əvəz edirsiniz.
4. Get Names düyməsinə basırsınız.

**Nümunə 2**

Siz son 1 ayda sizə qarşı mənfi fikir yazan şəxsləri müəyyənləşdirmək istəyirsiniz.

1. "Hacker mode"u yandırırsınız.
2. Tarix aralığını son 1 ayı əhatələyəcək şəkildə seçirsiniz.
3. Söz siyahısına təxmin etdiyiniz mənfi sözləri(vulqar ifadələr, təhqir və s.) yazırsınız.
4. Get Names düyməsinə basırsınız.

## Quraşdırma
Əgər quraşdırılmayıbsa [buradan](https://nodejs.org/en/) Node.js yükləyin.
Daha sonra terminalı açıb kodların yerləşdiyi baş qovluğa keçin. Aşağıdakı sətr qovluğu yüklədiyiniz yerdən asılı olaraq fərqli ola bilər:
```bash
cd [baş qovluğun ünvanı]
```

Kodla işləməzdən öncə lazımi kitabxanaları yükləyin:
```bash
npm install
```
Kodlarla işləyən zaman dəyişikliklərin canlı tətbiq olunması üçün proqramı **lokal mühitdə** (öz kompüterinizdə) aşağıdakı əmr ilə işə salın və terminalda çıxan [linkə](https://localhost:3000) daxil olun:
```bash
npm run dev
```
Proyekti hostinq mühitində bir server kimi qaldırmaq istəyirsinizsə onda yuxarıdakı əmr əvəzinə **hostinq mühitində** bu sətirləri bir-birinin ardınca icra edin:
```bash
npm run generate
npm run start
```
Əgər hostinqinizdə terminala çıxışınız yoxdursa və birbaşa hazır faylları(HTML, CSS, Javascript) köçürmək istəyirsinizsə onda **lokal mühitdə** aşağıdakı əmri icra edin:
```bash
npm run generate
```
Yaradılan faylları baş qovluğun içərisindəki `dist` qovluğunda tapa bilərsiniz.

## Facebook tətbiqinin inteqrasiyası
Sayta öz Facebook tətbiqinizi inteqrasiya etmək üçün `app.html` faylında, `<script>` teqi içərisindəki `appId` nömrəsini Facebook tərəfindən sizin tətbiqə verilmiş nömrə ilə əvəz edin. Facebook tətbiqinin quraşdırılması ilə bağlı ətraflı məlumatı [buradan](https://developers.facebook.com/docs/development) əldə edə bilərsiniz.

### SSL
Facebook tətbiqləri SSL(HTTPS) aktiv edilməyən saytları dəstəkləmir. [Cloudflare](https://www.cloudflare.com/ssl/) vasitəsilə saytınız üçün pulsuz SSL sertifikat əldə edə bilərsiniz. `localhost.crt` sertifikatından istifadə edən zaman isə brauzerinizin təhlükə xəbərdarlığı verməsi normaldır. Server lokal mühitdə qaldırıldığı halda xəbərdarlığı nəzərə almadan sayta daxil olun.

### İcazələr
Proqramın, istifadəçilərin Facebook məlumatlarına çıxış əldə edə bilməsi üçün Facebook tətbiqinizin aşağıdakı icazələri aldığına əmin olun:
- `pages_messaging`
- `pages_manage_metadata`
- `pages_read_engagement`

**Qeyd:** `pages_messaging` icazəsinin verilməsi üçün yaratdığınız hər hansı bir səhifə üçün müvəqqəti *webhook* quraşdırmalısınız. Bu `webhook` yoxlanma əsnasında səhifənizə göndərilən mesajlara avtomatik cavablar verə bilməlidir. Ətraflı təlimatla [buradan](https://developers.facebook.com/docs/messenger-platform/getting-started) tanış ola bilərsiniz.

**Qeyd 2:** Facebook tərəfindən verilən icazələr son 90 gün ərzində istifadə edilmədiyi təqdirdə geri alınır. Bu halda icazələri bərpa etmək üçün yenidən müraciət göndərməli olacaqsınız.

Yuxarıdakı icazələrdən əlavə, tətbiqin Facebook tərəfindən təsdiqlənməsi də lazımdır. Tətbiqinizi fərdi proqramçı kimi təsdiqlətdiyiniz halda passportunuzu göstərməniz kifayət olacaq. Ətraflı məlumatı [buradan](https://developers.facebook.com/docs/app-review) əldə edə bilərsiniz.

Ümumilikdə icazə və təsdiqlənmə müraciətlərinizə Facebook tərəfindən bir neçə saat ərzində cavab verilir.

## Planlaşdırılır
- [ ] Ad siyahısının səhifədə avtomatik dərc olunması

## Məxfilik
Tətbiqin normal fəaliyyəti üçün istifadəçi Facebook hesabından giriş etməli və istənilən icazələri təsdiqləməlidir.
Server özündə istifadəçiyə dair heç bir şəxsi məlumatı işləmir, saxlamır. Bütün məlumat prosessinqi istifadəçinin cihazında həyata keçirilir, serverə heç bir şəxsi məlumat göndərilmir.

## Məhdudiyyətlər
Facebook, tətbiqlərin yalnız *səhifə* mesajlarını oxumasına icazə verir. Sayt vasitəsilə *şəxsi* mesajlarınızı analiz edə bilməzsiniz.

## Lisenziya
Proqram kodlarından istifadə MIT lisenziyasına əsasən tənzimlənir.
