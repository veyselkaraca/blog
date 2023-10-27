---
title: Node-RED'e Kimlik Doğrulama Eklemek
tags:
- node-red
- IoT
- Authentication
thumbnail-img: assets/img/node-red.png
New field 1: node-red-e-kimlik-dogrulama-eklemek
---

Node-RED, IoT projelerinden veri analitiğine kadar birçok kullanım alanında güçlü bir akış tabanlı geliştirme aracıdır. Ancak, Node-RED'in yönetim arabirimine erişimi kısıtlamak ve güvence altına almak istiyorsanız, kimlik doğrulama eklemek önemlidir. Bu blog yazısında, Node-RED'in yönetim arabirimine basit bir kimlik doğrulama nasıl eklenir adım adım açıklanacaktır.

### 1. Node-RED'i Durdurun:
Önce Node-RED'in çalıştığınız sunucu veya cihazda çalışmasını durdurun. Aşağıdaki komutu kullanabilirsiniz:

`node-red-stop`


### 2. Ayar Dosyasını Düzenleyin:

Node-RED ayar dosyasını açın. Bu dosya genellikle settings.js olarak adlandırılır ve Node-RED'in ana dizininde bulunur. Eğer bulmakta sorun yaşıyorsanız node-red'in [dokümanlarını](https://nodered.org/docs/user-guide/runtime/settings-file) kontrol edeblirsiniz. Metin düzenleyici kullanarak bu dosyayı açın.



### 3. Kimlik Doğrulama Ayarlarını Ekleyin:
settings.js dosyasında, adminAuth bölümünü düzenleyin ve aşağıdaki ayarları ekleyin:


```javascript
adminAuth: {
   type: "credentials",
   users: [{
       username: "kullanici_adi",
       password: "sifre",
       permissions: "*"
   }]
}
```

### 4. Node-RED'i Yeniden Başlatın:
Settings.js dosyasındaki değişiklikleri kaydedin ve Node-RED'i yeniden başlatın:

```bash
node-red-start
```

#### Sonuç:
Artık Node-RED yönetim arabirimine erişmeye çalıştığınızda, "kullanici_adi" ve "sifre" ile kimlik doğrulama gerekecektir. Bu basit adımlarla Node-RED yönetim arabirimini güvence altına alabilirsiniz.
![]({{ 'assets/img/node-red_authentication_screen.png' | relative_url }})

#### Son Notlar:

* Güçlü ve benzersiz şifreler kullanmaya dikkat edin.
* Kimlik bilgilerinizi güvenli bir şekilde saklayın.
* Gerçek bir uygulama için daha fazla güvenlik önlemi gerekebilir.

#### Kaynaklar;
- [Secure Node-RED](https://nodered.org/docs/user-guide/runtime/securing-node-red)
- [Node-RED Settings File](https://nodered.org/docs/user-guide/runtime/settings-file)
