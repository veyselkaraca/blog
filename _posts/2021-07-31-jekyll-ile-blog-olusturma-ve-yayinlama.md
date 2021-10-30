---
title: Jekyll ile Blog Oluşturma ve Yayımlama
permalink: jekyll-ile-blog-olusturma-ve-yayinlama
author: veysel karaca
thumbnail-img: /assets/img/Jekyll_(software)_Logo.png
tags: websitegenerator
---
Merhaba. Bloğumun ilk yazısı olan Jekyll ile Blog Oluşturma ve Yayımlama yazıma hoşgeldiniz. Başlıktan da anlaşılacağı üzere bugün bu bloğu kurarken de kullanmış olduğum Jekyll statik site oluşturucusu ile bir blog sitesi oluşturup bunu github student pack sayesinde namecheap domain servisleri ile yayımlayacağız.

# Öncelikle Jekyll ile Tanışalım
Jekyll Ruby Programlama Dili ile geliştirmiş, açık kaynak bir statik site oluşturucudur (Static Site Generator). Jekyll ile hızlıca web sitesi oluşturabilir ve yayımlayabilirsiniz.

Elbette her sorunu çözen sihir bir değnek olmakdığı hatırlamamız gerekli. Jekyll ağırlı olarak; blog, cv, iletişim sitesi, etkinlik sitesi, dökümantasyon sitesi gibi içeriğin webadmin tarafından oluşturulduğu ve kullanıcıyla daha az etkileşime girildiği web siteleri için etklidir. Ne yazık ki Jekyll ile bir e-ticaret sitesi geliştiremezsiniz. Bunun sebebi ise onun bir static site generator olmasındandır.




# Jekyll - Static Site Generator
Jekyll en başta bahsettiğimiz gibi Ruby programlama dile geliştirilmiş bir Static Site Generator. Ancak Jekyll kullanırken Ruby dili bilmenize gerek yoktur. Yalnızca bazı yazım kurallarını bilmeniz sizin için yeterlidir.

Bu öğreticide Jekyll ile nasıl web sitesi oluşturulacağını inceleyeceğiz.

Bilinmesi Gerekenler;

Markdown: Bir markup dilidir. Şuan okumuş olduğunuz bu blog yazısı markdown dilinde yazılmış ve HTML'e dönüştürülerek sizlere sunulmuştur. HTML'e oranla çok daha kolay yazılabilen ve okunabilen bir markup dilidir. Jekyll'de içeriklerinizi markdown dosyası olarak oluşturmanız gerekmektedir. Uzantısı .markdown ya da .md'dir. Ayrıca markdown içerisine HTML kodları eklenebilir. Bu sayede çok daha güzel görünümlü içerikler elde edilebilir.

YAML: Bir başka markup dilidir. Jekyll bu dili _config.yml dosyasında içerikleri oluşturduğunuz markdown dosyalarında kullanmaktadır. Tıpkı markdown gibi kolay okunabilen ve yazılabilen bir yapıya sahiptir. Markdown dosyalarının içinde içeriklerin meta bilgilerini yazmak için kullanılır. Uzantısı .yaml ya da .ymldır.

Ancak bunlardan korkmanıza gerek yok markdown ve yaml markup dilleri kolay öğrenebileceğiniz hatta internette 5 dakikada öğrenebileceğiniz web siteleri dahi var.
Bunlardan bir kaçı;   
[Markdown](https://www.markdowntutorial.com/)   
[Yaml](https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started)

# Jekyll Kurulumu Gereksinimler

Ruby v2.4.0 ya da üstü

RubyGems

Windows'da Ruby kurulu için en çok tercih edilen yol RubyInstaller kullanmaktır. Eğer Windows kullanıyorsanız ve daha önce Ruby dili ilgilenmediyseniz [RubyInstaller](https://rubyinstaller.org/downloads/) kullanmanızı öneririm. RubyGems'de RubyInstaller ile birlikte kurulacaktır.
Bu yazıda ben Ruby'nin 3.2.0 versiyonunu kullanacağım

Ruby ve RubyGems kurulumu tamamlandıktan sonra terminal ekranında aşağıda komutu çalıştırarak Jekyll kurulumunu tamamlayabilirsiniz.


`gem install jekyll bundler`


Daha detaylı kurulum bilgisi için lütfen Jekyll Installation sayfasına göz atınız.

Jekyll Projesi Oluşturma ve Dosya Yapısı
Bütün kurulumlar sorunsuz olarak tamamlandıysa Jekyll projesini oluşturmaya başlayabilirsiniz. Kaynak kodları saklayacağız dizine gittikten sonra aşağıdaki komut ile jekyll projesi oluşturulacaktır.

`jekyll new myblog`

Burada yazan 'myblog' yerine istediğiniz herhangi bir adı verebilirsiniz. Ancak boşluk karakteri kullanmaktan kaçınınız. Onun yerine _ (alt tire) kullanabilirsiniz. Best practice olarak ad kısmınında küçük harfler kullanmanız tavsiye edilir.

Herhangi bir metin editörü ile projeyi açtığınızda aşağıdaki gibi bir dosya yapısı ile karşılaşacaksınız.

myblog  
--404.html  
--about.markdown  
--_config.yml  
--Gemfile  
--Gemfile.lock  
--index.markdown  
-- _posts  
----20210110-welcome-to-jekyll.markdown

Dosyalar ve Dizinler;

**404.html:** 404 hatası yaşandığı durumda kullanıcı tarafından görüntülecek dosyadır.

**about.markdown:** Default oluşturulmuş 'about' sayfasının içeriğidir.

**_config.yml:** Jekyll projesinin yapılandırma ayarlarının bulunduğu dosyadır.

**index.markdown:** Default oluşturulmuş 'index' sayfasının içeriğidir. Projenizde 'index' dosyası bulunmanız tavsiye edilir. Eğer kullanmak istemiyorsanız _config.yml dosyası içerisindeki baseurl kısmına anasayfa olarak belirlemek istediğiniz sayfayı yazabilirsiniz.

**_posts:** Bu dizin adı default oluşturulmuştur. Dizinin adını değiştirebilir ya da bunun gibi yeni dizinler oluşturabilirsiniz. Bu dizinler kategori gibidir ve yazılarınızı bu dizin içerisine ekleyebilirisiniz. Bu sayede dizin içerisindeki yazılarınız bu dizine bağlanmış olur.

**'_config.yml' Dosyası**

Bu dosya jekyll projesinin global bilgilerini ve ayarlarını barındırır. Aşağıdaki çıktı oluşturmuş olduğumuz proje içerisinde By-Default olarak yazılan bilgilerdir. Bu dosya eklediğimiz pluginler, temalar ve daha bir çok bilgiyi içermektedir.

```
title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: jekyllrb
github_username:  jekyll

# Build settings
theme: minima
plugins:
  - jekyll-feed
```
# Jekyll İle Statik Dosyaların Oluşturulması ve Deployment

Herşey hazır gibi gözüküyor ama Ruby 2.7 üzerinde bir sürüm kullanıyorsanız webrick artık Ruby ile beraber gelmediği için onu manuel olarak kendiniz eklemeniz gerekiyor. Yardımcı olacağını düşündüğüm bir [stackoverflow linki](https://stackoverflow.com/questions/65989040/bundle-exec-jekyll-serve-cannot-load-such-file) bırakarak yazıma devam ediyorum 😊

Artık Jekyll'ın asıl olayı olan statik dosyaların oluşturulması kısmına geldik. Bunun için aşağıdaki komutları terminalde çalıştırarak statik dosyaların oluşturulmasını sağlayabilirsiniz.

```
cd myblog
bundle install
bundle exec jekyll serve
```
Komutları çalıştırdıktan sonra 4000 portunda bir servis oluşturarak sitemizin oluşturulmuş halini görüntüleyebiliriz.

![]({{ 'jeckyll_home_page.png' | relative_url }})

Aynı zamanda proje dizininde yeni eklemeler oldu. _site dizininde markdown dosyalarımız _config.yml dosyasındaki ayarlamıza göre HTML olarak oluşturuldu. Eğer ki web sitemizi canlıya almak istersek yalnızca '_site' dizininin altındaki dosyaları sunucuya yüklemek yeterli olacaktır. Bu sayede tamamen statik bir web sitesini kullanıcılara sunabiliriz.

# Jekyll İle Blog Sitesi Oluşturma

Jekyll Themes sayfasını kullanarak beğendiğiniz bir tema ile başlayabilirsiniz.. Kaynak kodlar MIT Lisansı ile lisanslandığı için değiştirmekte ve kullanmakta tamamen özgürüz 😊

Github sayfasından kaynak kodlarını indiriyoruz ve herhangi bir editör ile kodları açıyoruz.

```
git clone https://github.com/cotes2020/jekyll-theme-chirpy/
cd jekyll-theme-chirpy/
code .
```
Burada ilk yapmamız gereken _config.yml dosyası içerisindeki bilgileri değiştirmek. Tema geliştiricisi bizim için yorum satırları eklemiş ve geriye yalnızca uygun alanları doldurmak kalıyor.
```

title: Veysel Karaca                          # the main title

tagline: Software Developer   # it will display as the sub-title

description: >-                        # used by seo meta and the atom feed
  Veysel Karaca kişisel web sitesi ve teknik blog sayfası

# fill in the protocol & hostname for your site, e.g., 'https://username.github.io'
url: ''

author: Veysel Karaca                  # change to your full name

github:
  username: veyselkaraca             # change to your github username

twitter:
  username: veyselkrc            # change to your twitter username

social:
  name: Veysel Karaca                  # it will shows as the copyright owner in Footer
  email: veyselkaraca.contact@gmail.com             # change to your email address
  links:
    # The first element serves as the copyright owner's link
    - https://www.linkedin.com/in/veyselkaraca/
    - https://twitter.com/veysellkrc      # change to your twitter homepage
    -https://github.com/veyselkaraca       # change to your github homepage
    - https://www.instagram.com/veysell.krc

baseurl: ''

# Change to your timezone › http://www.timezoneconverter.com/cgi-bin/findzone/findzone
timezone: Europe/Istanbul
```

Herşey hazır gibi görünüyor. Artık statik dosyaları elde etme vakti;

```
bundle install
bundle exec jekyll serve
```

Jekyll gibi farklı dillerde gelişirilmiş yüzlerce statik site oluşturucusu mevcuttur. Meraklıları[ bu](https://jamstack.org/generators/) sayfaya göz atabilir 😊
# Site Yayımlama

Herşey hazır gibiyse eğer sıra sitemizi yayına almaya geldi . Github'ın nimetlerinden yararlanma zamanı [bu](https://education.github.com/pack) linke tıklayarak namecheap sitesini bulun

![]({{ 'github_student_namecheap.png' | relative_url }})

github hesabınızı namecheamp hesabınıza bağlayarak giriş yapın ve ücretsiz bir .me domaini alabilirsiniz (1 yıl geçerlidir) 

Eğer bir sorun yaşarsanız benimle iletişime geçmekten çekinmeyin

Herşey bu kadar basitti 😊


Yazılım ile kalın!
