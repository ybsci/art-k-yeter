---
title: Windows WSL2 ile Linux Kerneline Destek Veriyor
date: 2020-08-11T15:42:21.744Z
lastmod: 2020-08-11T15:42:21.815Z
draft: false
categories:
  - WSL
tags:
  - WSL
  - Linux
  - Windows
author: Yakup Ataş
description: Ne dediğinizi duyar gibiyim. Bende ilk duyduğumda öyle demiştim.
  Microsoft açık kaynak verilerine destek vermesi bana çok garip geldi ama
  yapmış, şaşırtıcı. Windows bu desteği sunması bize nasıl bir fayda sağlayacak?
hiddenFromHomePage: false
hiddenFromSearch: false
lightgallery: false
featuredImagePreview: images/windows.webp
---
Ne dediğinizi duyar gibiyim. Bende ilk duyduğumda öyle demiştim. Microsoft açık kaynak verilerine destek vermesi bana çok garip geldi ama yapmış şaşırtıcı. Windows bu desteği sunması bize nasıl bir fayda sağlayacak?

Hala yaygın olarak kullanılan sanal makine kurma ile istenilen her işletim sistemi windowsa kurulabilir fakat bu biraz zahmetli ve uğraştırıcı bir yoldur. Bunu yapmak için bilgisayarınıza virtualbox kurmanız ve sanal makineyi aktif etmeniz için, kullanmak istediğiniz linux dağıtımını indirmeniz gerekir. Genel de yeni kullanıcılar için biraz zahmetli bir yoldur ve kaynak kullanımı fazladır. Tabi Sanal makine de ayarladığınız kaynak kadar kaynak tüketir. Kurarken size sorar bu sanal makine için kaç GB ram kullanılsın diye.. virtualbox üçüncü taraf bir yazılım olduğu için bozulma ve kaydedilen verilerin kaybolma ihtimali de vardır. BU sebepten dolayı verilerinizin kaybolması ve bozulması ihtimali vardır.Tabi bu verileri kurtarabilirsiniz ama araştırmalarıma göre biraz zahmetli bir yol.

Microsoft, windows 10 2004 güncellemesiyle gelen WSL(Windows Subsystem For Linux) teknolojisiyle, yukarıda bahsettiğim adımları kullanmadan bir linux dağıtımını windows üzerinden kullanmanızı sağlayan bir sistemdir.

Windows ve Linux temelde donanımla haberleşirken farklı yöntemler kullanılmaktadır. Yani Linux donanım ile haberleşirken kullandığı arka plan işlemleri, windowsun kullandığı işlemler arasında farklılıklar olduğu kesin. hoş linux hangi işlemleri kullanıyor biliyoruz ama mesele windows olunca arka planda neler yapıyor en ufak bir fikrimiz yok.Çünkü açık kaynak bir yazılım değil. Windows ve para ayrılmaz ikililer:D. Windows bu problemi çözmek için arka planda bir sanallaştırma teknolojisi kullanmış. Okuduğum yorumlara ve araştırmalarda, sanal makineye göre daha stabil ve performanslı çalışmaktadır. Ehh okadar para kazanıyorsun bir zahmet olsun diyenlerdenseniz emin olun doğru yoldasınız.

**Hadi gelin kurulum detaylarına geçelim.**

## Adım Adım

### 1. Windows Güncelleme

Öncelikle windows 10 sürümünüzün 2004 olması gerekir. eğer değilse yükseltme yapmadan kurmanızı tavsiye etmiyorum. Çünkü 2004 ten önceki sürümler WSL1 teknolojisi kullanıyor ve bu teknoloji linux kerneline destek vermemektedir. Eğer sisteminizin sürümünü bilmiyorsanız arama kısmına:
`winver`

![Windows Hakkında](/images/winver.webp "Windows Hakkında")

Eğer sisteminiz resimde görünen gibi güncel değil ise güncelleyin.

### 2. WSL Yükleme

Windows arama çubuğuna powersell yazıp, yönetici olarak çalıştırınız.
`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`

![WSL Yükleme](/images/adım1.webp "WSL Yükleme")

Bu terminal kodunu kopyalayıp powerselle yapıştırıp enter’a basınız. bu komut WSL’i aktif hale getirecektir.

### 3. Bilgisayarınızı Yeniden Başlatın.

### 4. Sanal Makineyi Aktif Etme

Windows arama çubuğuna powersell yazıp, yönetici olarak çalıştırınız.

`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

![Sanal Makine aktif etme](/images/adım2.webp "Sanal makineyi aktif etme")

Bu komut bilgisayarınızda sanal makineyi kullanım için aktif hale getirecektir.

### 5. Sanal Makine için WSL2 Aktif Etme

`dism.exe
Linux /all /norestart`

![WSL2 Aktif Etme](/images/adım3.webp "WSL2 Aktif Etme")

### 6. Bilgisayarınızı yeniden başlatın.

### 7. Linux Kernelini İndirme

<https://aka.ms/wsl2kernel> linkine giderek WSL linux kernelini indirin ve kurun.

![Kernel İndirme](/images/7.adım.webp "Kernel İndirme")

### 8. WSL Default Olarak Ayarlama

Windows arama çubuğuna powersell yazıp, yönetici olarak çalıştırınız.

`wsl --set-default-version 2`

![WSL Default Ayarlama](/images/adım-8.webp "WSL Default Ayarlama")

Bu komutu kopyalayıp powershellde çalıştırınız. Bu komut WSL2'yi default olarak uygulanacaktır.

### 9. WSL VarOlan GNU/Linux İşletim Sistemlerinini Görme

Powershell komutu:`wsl --list --verbose`

![WSL Var Olan Linux İşletim Sistemlerinini Görme](/images/adim-9.webp "WSL Var Olan Linux İşletim Sistemlerinini Görme")

Bilgisayarınızda var olan makineleri listeler. 

### 10. Linux İndirmek

Microsoft mağazasına giderek istediğiniz Linux dağıtımını indiriniz. Garip mi geldi bana da ben Kali Linux'u indirdim ve kurdum.

![Linux İndirmek](/images/adım-10.webp "Linux İndirmek")

Uygulamayı başlattığınız esnada bilgisayarda terminal ekranı önünüze gelecektir.

![Terminal](/images/adım11.webp "Terminal")

Çekinmeyin korkacak bir şey yok, şimdi kendinize bir kullanıcı adı ve şifre seçin eğer sürekli kullanacaksanız lütfen unutmayacak şeyler seçin malum Linux eğer parola bilmiyorsanız size zırnık koklatmaz😀

## Kali linux Arayüzünü Yükleme

WSL ile kali linux terminalini istediğiniz gibi kullanabilirsiniz. Fakat ben arayüz görmek istiyorum bu şekil çok çirkin derseniz Sorun yok arayüzünü hemen yükleyebiliriz. Hemen değilde Koca bir arayüz indireceksiniz terminal üstünden biraz beklemeniz gerekecek:)

### 1. Sistem Güncellemesi

`sudo apt update && sudo apt upgrade -y`

![Sistem Güncellemesi](/images/adım12.webp "Sistem Güncellemesi")
komutunu yapıştırıp enter’a tıklayınız.Linux terminalinde kopyala yapıştır ctrl+shift+v ile yapılır normalde fakat burda, kopyaladıktan sonra mouse de sağ tıklayarak yapabilirsiniz. Olmadıysa elle yazın artık 🙂 bu yapının inmesi biraz zaman alacaktır

### 2. Xfce Pencere Yöneticisini İndirmek

`sudo apt install kali-desktop-xfce -y`

Bu komut arayüzü indirip kuracaktır.

İndirme esnasında isterseniz şuan bilgisayarınızda var olan makinelerin durumunu  incelemek için , windows powershell’ ine:`wsl --list --verbose` komutunu çalıştırıp görebilirsiniz.

### 3. Xrdp'yi İndirmek

Şimdi kurduğumuz Kali Linux arayüzüne ulaşmak için uzaktan kontrol etme bağlantısını kullanarak bağlanalım bunun için Linux terminali için xrdp kurmamız gerekir.( Remote desktop Connetion: Windows üzerinden çalışan başka bir internete bağlı windows cihazına bağlanmanızı sağlayan bir teknoloji, Xrdp Linux makinelere bağlanmanızı sağlar).
`sudo apt install xrdp -y` bu komut bilgisayarınıza Xrdp'yi kuracaktır.

### 4. Xrdp Servisini Başlatmak

Linux terminaline: `sudo service xrdp start` komutunu çalıştırın. Xrdp başlamış olacaktır.

### 5. IP adresini Öğrenme

Terminale: `ip add` komutu ile öğrenin ve not alın. 

![IP Adresi Öğrenme](/images/adim21ı-1.webp "IP Adresi Öğrenme")

### 6. Uzak Masaüstü Bağlantısı(RDP) Açmak

Windows arama kısmında uzak masaüstü bağlantısı(RDP) yazarak aratırsanız sizden ip isteyen bir arayüz gelecektir. Oraya not aldığınız ip adresini yazın, bağlana tıklayın. Önünüze xrdp arayüzü açılacak buraya Linux kurulumu yaparken kullandığınız kullanıcı adı ve parolayı giriniz.

Kali kinux terminalini açıp istediğiniz programı yükleyebilir ve işlemler yapabilirsiniz.