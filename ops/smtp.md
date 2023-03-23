# Aga seva ya gago ya go romela poso ya SMTP

## ketapele

SMTP e ka reka ditirelo ka go lebanya go tšwa go barekiši ba leru, go swana le:

* [Amazon SES SMTP ya go swana le yona](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali leru imeile kgorometsa](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

O ka boela wa ikagela seva ya gago ya poso - go romela mo go sa lekanyetšwego, theko ya fase ka kakaretšo.

Ka fase, re bontšha kgato ka kgato ka moo re ka agago seva ya rena ya poso.

## Kgetho ya seva

Seva ya SMTP yeo e išwahlelago e nyaka IP ya setšhaba yeo e nago le dikou tša 25, 456, le 587 tšeo di bulegilego.

Maru a setšhaba ao a šomišwago ka tlwaelo a thibetše maemakepe a ka go ikemela, gomme go ka kgonega go a bula ka go ntšha taelo ya mošomo, eupša go a tshwenya kudu ka morago ga tšohle.

Ke kgothaletša go reka go tšwa go moamogedi yo a nago le dikou tše tše di bulegilego gomme di thekga go hloma maina a domain ya go bušetša morago.

Mo, ke kgothaletša [Contabo](https://contabo.com) .

Contabo ke moabi wa go amogela baeng yo a lego Munich, Jeremane, yo a hlomilwego ka 2003 ka ditheko tša phadišano kudu.

Ge o kgetha Euro bjalo ka tšhelete ya go reka, theko e tla ba theko e tlase (seva yeo e nago le memori ya 8GB le di-CPU tše 4 e bitša mo e ka bago 529 yuan ka ngwaga, gomme tefo ya mathomo ya go hloma ke ya mahala ka ngwaga o tee).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Ge o bea taelo, hlokomela `prefer AMD` , le seva le AMD CPU tla ba le tshebetso molemo.

Go tše di latelago, ke tla tšea VPS ya Contabo bjalo ka mohlala go bontšha ka moo o ka ikagelago seva ya gago ya poso.

## Peakanyo ya tshepedišo ya Ubuntu

Tshepedišo ya go šoma mo ke Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ge e ba seva go ssh e bontšha `Welcome to TinyCore 13!` (bjalo ka ge go bontšhitšwe seswantšhong se se lego ka mo tlase), go ra gore tshepedišo ga se ya hlongwa ga bjale. Hle kgaola ssh gomme o eme metsotso e sego kae gore o tsene gape.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ge `Welcome to Ubuntu 22.04.1 LTS` e tšwelela, go thoma go phethilwe, gomme o ka tšwela pele ka magato a a latelago.

### [Kgetho] Thoma tikologo ya tlhabollo

Mohato wo ke wa boikgethelo.

Bakeng sa go ba bonolo, ke beile go hloma le peakanyo ya tshepedišo ya softwere ya ubuntu go [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Matha taelo ye e latelago go tsenya ka go klika ga tee.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Badiriši ba Setšhaena, hle diriša taelo ye e latelago go e na le moo, gomme polelo, lefelo la nako, bjalobjalo di tla bewa ka go iketla.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo e kgontšha IPV6

Kgontšha IPV6 gore SMTP e kgone go romela gape di-imeile tšeo di nago le diaterese tša IPV6.

rulaganya `/etc/sysctl.conf`

Fetoša goba o oketše methalo ye e latelago

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Latela ka [thuto ya contabo: Go tlaleletša kgokagano ya IPv6 go seva ya gago](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Edit `/etc/netplan/01-netcfg.yaml` , eketsa mela e seng mekae joalokaha ho bontšitsoe setšoantšong ka tlase (Contabo VPS default peakanyo faele e se e na le mela ena, feela uncomment bona).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Ke moka `netplan apply` go dira gore peakanyo ye e fetotšwego e šome.

Ka morago ga ge peakanyo e atlegile, o ka šomiša `curl 6.ipw.cn` go lebelela aterese ya ipv6 ya netiweke ya gago ya ka ntle.

## Clone ya phetolo polokelo ops

```
git clone https://github.com/wactax/ops.soft.git
```

## Hlagiša setifikeiti sa mahala sa SSL sa leina la gago la domain

Go romela poso go nyaka setifikeiti sa SSL bakeng sa go šitiša le go saena.

Re šomiša [acme.sh](https://github.com/acmesh-official/acme.sh) go tšweletša disetifikeiti.

acme.sh ke mohlodi o bulehileng jarolla ka ho iketsa setifikeiti saena sesebediswa, .

Kenya polokelo ya peakanyo ops.soft, matha `./ssl.sh` , gomme foltara ya `conf` e tla hlolwa ka **go tšhupetšo ya ka godimo** .

Hwetša moabi wa gago wa DNS go tšwa go [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , rulaganya `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Ebe matha `./ssl.sh 123.com` go tšweletša disetifikeiti tša `123.com` le `*.123.com` bakeng sa leina la gago la domain.

The pele matha tla ka tsela e iketsang kenya [acme.sh](https://github.com/acmesh-official/acme.sh) le eketsa mosebetsi o hlophisitsoeng bakeng sa nchafatso jarolla ka ho iketsa. O ka bona `crontab -l` , ho na le mola o joalo ka tsela e latelang.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Tsela ya setifikeiti seo se tšweleditšwego ke selo se sengwe sa go swana le `/mnt/www/.acme.sh/123.com_ecc。`

Mpshafatšo ya setifikeiti e tla bitša sengwalwa sa `conf/reload/123.com.sh` , rulaganya sengwalwa se, o ka oketša ditaelo tša go swana le `nginx -s reload` go hlabolla cache ya setifikeiti ya dikgopelo tše di amanago.

## Haha seva ya SMTP ka chasquid

[chasquid](https://github.com/albertito/chasquid) ke seva ya SMTP ya mohlodi o bulegilego yeo e ngwadilwego ka polelo ya Go.

Bjalo ka legato la mananeo a bogologolo a seva ya poso a go swana le Postfix le Sendmail, chasquid e bonolo ebile e bonolo go e šomiša, gomme gape e bonolo bakeng sa tlhabollo ya bobedi.

Matha `./chasquid/init.sh 123.com` e tla tsenywa ka go itiriša ka go kgotla ga tee (tšeela 123.com sebaka ka leina la gago la domain la go romela).

## Beakanya DKIM ya Mosaeno wa Imeile

DKIM e šomišwa go romela ditshaeno tša imeile go thibela mangwalo go swarwa bjalo ka spam.

Ka morago ga ge taelo e sepele ka katlego, o tla kgopelwa go beakanya rekoto ya DKIM (bjalo ka ge go bontšhitšwe ka mo tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

E no oketša rekoto ya TXT go DNS ya gago (bjalo ka ge go bontšhitšwe ka mo tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Lebelela maemo a tirelo & dilog

 `systemctl status chasquid` Sheba boemo ba tšebeletso.

Boemo ba tshebetso e tloaelehileng ke joalokaha ho bontšitsoe setšoantšong ka tlase

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` goba `journalctl -xeu chasquid` e ka lebelela log ya phošo.

## Bušetša morago peakanyo ya leina la domain name

Leina la domain la go bušetša morago ke go dumelela aterese ya IP go rarollwa go leina la domain leo le swanetšego.

Go beakanya leina la domain la go bušetša morago go ka thibela di-imeile go hlaolwa bjalo ka spam.

Ge poso e amogetšwe, seva ye e amogelago e tla dira tshekatsheko ya leina la domain ya go bušetša morago atereseng ya IP ya seva ye e romelago go tiišetša ge e ba seva ye e romelago e na le leina la domain ya go bušetša morago ye e šomago.

Ge e le gore seva ye e romelago ga e na leina la domain ya go bušetša morago goba ge leina la domain la go bušetša morago ga le swane le aterese ya IP ya seva ye e romelago, seva ye e amogelago e ka lemoga imeile bjalo ka spam goba ya e gana.

Etela [https://my.contabo.com/rdns](https://my.contabo.com/rdns) gomme o beakantše bjalo ka ge go bontšhitšwe ka mo tlase

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Ka morago ga go beakanya leina la domain la go bušetša morago, gopola go beakanya tharollo ya pele ya leina la domain ipv4 le ipv6 go seva.

## Edita leina la moamogedi wa chasquid.conf

Fetoša `conf/chasquid/chasquid.conf` go boleng bja leina la domain la go bušetša morago.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Ebe matha `systemctl restart chasquid` ho qala tšebeletso hape.

## Backup conf go polokelo ya git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Mohlala, ke dira bekapo ya foltara ya conf go tshepedišo ya ka ya github ka tsela ye e latelago

Theha polokelo ya poraefete pele

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Kenya conf directory gomme o romele polokelong

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Oketša moromiši

kitima

```
chasquid-util user-add i@wac.tax
```

A ka oketša moromiši

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Netefatša gore phasewete e beakantšwe gabotse

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Ka morago ga go oketša mosediriši, `chasquid/domains/wac.tax/users` e tla mpshafatšwa, gopola go e romela polokelong.

## DNS eketsa rekoto ya SPF

SPF ( Sender Policy Framework ) ke theknolotši ya netefatšo ya imeile yeo e šomišwago go thibela bomenetša bja imeile.

E netefatša boitšhupo bja moromiši wa poso ka go lekola gore aterese ya IP ya moromiši e swana le direkhoto tša DNS tša leina la domain leo e ipolelago gore ke lona, ​​e thibela boradia go romela di-imeile tša bofora.

Go oketša direkhoto tša SPF go ka thibela di-imeile go hlaolwa bjalo ka spam ka mo go kgonegago.

Ge e le gore seva ya gago ya leina la domain ga e thekge mohuta wa SPF, e no oketša rekoto ya mohuta wa TXT.

Ka mohlala, SPF ya `wac.tax` e ka tsela e latelang

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF bakeng sa `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Hlokomela gore ke na `include:_spf.google.com` mo, se ke ka gobane ke tla beakanya `i@wac.tax` bjalo ka aterese ya go romela ka lepokising la poso la Google ka morago.

## DNS peakanyo DMARC

DMARC ke khutsofatšo ya (Netefatšo ya Molaetša wo o theilwego go Domain, Go Bega & Tumelelano).

E šomišwa go swara di-bounce tša SPF (mohlomongwe di hlolwa ke diphošo tša peakanyo, goba motho yo mongwe o itira eka ke wena go romela spam).

Oketša rekoto ya TXT `_dmarc` , .

Diteng ke tše di latelago

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Moelelo wa paramethara ye nngwe le ye nngwe ke ka tsela ye e latelago

### p (Pholisi) .

E laetša ka moo o ka swarago di-imeile tšeo di palelwago ke netefatšo ya SPF (Sender Policy Framework) goba DKIM (DomainKeys Identified Mail). Paramethara ya p e ka bewa go e nngwe ya dikelo tše tharo:

* ga go le e tee: Ga go kgato yeo e tšewago, ke sephetho sa netefatšo fela seo se bušetšwago morago go moromiši ka mokgwa wa go bega imeile.
* Kgethwa: Bea poso yeo e sego ya fetiša netefatšo ka gare ga foltara ya spam, eupša e ka se gane poso ka go lebanya.
* gana: Gana ka go lebanya di-imeile tšeo di palelwago ke netefatšo.

### fo (Dikgetho tša go palelwa) .

E laetša palo ya tshedimošo yeo e bušitšwego ke mokgwa wa go bega. E ka bewa go ye nngwe ya dikelo tše di latelago:

* 0: Bega dipoelo tša netefatšo ya melaetša ka moka
* 1: Bega fela melaetša yeo e palelwago ke netefatšo
* d: Bega fela go palelwa ga netefatšo ya leina la domain
* s: bega fela go palelwa ga netefatšo ya SPF
* l: Bega fela go palelwa ga netefatšo ya DKIM

### rua & ruf

* rua (Go bega URI ya dipego tša Aggregate): Aterese ya imeile ya go amogela dipego tše di kgobokeditšwego
* ruf (Go bega URI bakeng sa dipego tša Forensiki): aterese ya imeile go amogela dipego tše di tletšego

## Oketša direkhoto tša MX go fetišetša di-imeile go Google Mail

Ka lebaka la gore ke be ke sa kgone go hwetša lepokisi la poso la mahala la kgwebo leo le thekgago diaterese tša bokahohleng (Catch-All, e ka amogela di-imeile dife goba dife tšeo di rometšwego go leina le la domain, ntle le dithibelo tša dihlongwapele), ke šomišitše chasquid go fetišetša di-imeile ka moka go lepokisi la ka la poso la Gmail.

**Ge e ba o na le lepokisi la gago la poso la kgwebo leo le lefilwego, hle o se ke wa fetoša MX gomme o tlole kgato ye.**

Edita `conf/chasquid/domains/wac.tax/aliases` , beakanya lepokisi la poso la go fetišetša pele

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` e bontšha di-imeile ka moka, `i` ke hlogo ya aterese ya imeile ya mosebediši yo a romelago yo a hlotšwego ka mo godimo. Go fetišetša poso pele, modiriši yo mongwe le yo mongwe o swanetše go oketša mola.

Ebe eketsa rekoto ya MX (ke supa ka ho toba aterese ya lebitso la domain name la khutlisetsang mona, joalokaha ho bontšitsoe mola oa pele setšoantšong se ka tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Ka morago ga ge peakanyo e fedile, o ka šomiša diaterese tše dingwe tša imeile go romela di-imeile go `i@wac.tax` le `any123@wac.tax` go bona ge eba o ka amogela di-imeile ka go Gmail.

Ge e ba go se bjalo, hlahloba log ya chasquid ( `grep chasquid /var/log/syslog` ).

## Romela imeile go i@wac.tax ka Google Mail

Ka morago ga gore Google Mail e amogele poso, ka tlhago ke be ke holofela go araba ka `i@wac.tax` go e na le i.wac.tax@gmail.com.

Etela [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) gomme o kgotle "Oketša aterese ye nngwe ya imeile".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Ka morago ga moo, tsenya khoutu ya netefatšo yeo e amogetšwego ke imeile yeo e fetišeditšwego go yona.

Mafelelong, e ka bewa bjalo ka aterese ya moromiši ya go se fetoge (gotee le kgetho ya go araba ka aterese ye e swanago).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ka tsela ye, re phethile go hlongwa ga seva ya poso ya SMTP gomme ka nako ye e swanago re šomiša Google Mail go romela le go amogela di-imeile.

## Romela imeile ya teko go lekola ge eba peakanyo e atlegile

Kenya `ops/chasquid`

Matha `direnv allow` go tsenya ditshepetšo (direnv e hlomilwe ka tshepedišong ya pele ya go thoma ya senotlelo se tee gomme sekgoketšane se okeditšwe go khetla)

ke moka o kitime

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Moelelo wa ditekanyetos ke ka tsela e latelang

* mosebedisi: Lebitso la mosebedisi la SMTP
* feta: phasewete ya SMTP
* go: moamogedi

O ka romela imeile ya teko.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Go kgothaletšwa go šomiša Gmail go amogela di-imeile tša teko go lekola ge e ba dipeakanyo di atlegile.

### TLS maemo a encryption

Bjalo ka ge go bontšhitšwe seswantšhong se se lego ka mo tlase, go na le senotlelo se se nnyane, seo se ra gore setifikeiti sa SSL se kgontšhitšwe ka katlego.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Ebe tobetsa "Bontšha Imeile ya Mathomo".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Bjalo ka ge go bontšhitšwe seswantšhong se se lego ka mo tlase, letlakala la poso ya mathomo ya Gmail le bontšha DKIM, seo se ra gore peakanyo ya DKIM e atlegile.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Lekola Amogetšwe ka hlogong ya imeile ya mathomo, gomme o ka bona gore aterese ya moromiši ke IPV6, seo se ra gore IPV6 le yona e beakantšwe ka katlego.
