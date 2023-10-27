---
title: 'Docker Swarm vs. Kubernetes: Hangisi Daha İyi Bir Konteyner Orkestrasyon Çözümü?'
tags:
- DevOps
- Kubernetes
- Docker
thumbnail-img: assets/img/docker_swarm_vs_kubernetes.png
permalink: docker-swarm-vs-kubernetes-hangisi-daha-iyi-bir-konteyner-orkestrasyon-cozumu
---

Konteyner orkestrasyon çözümleri, günümüz uygulama dağıtımının temel taşları haline geldi. Ancak, Docker Swarm ve Kubernetes gibi farklı çözümler arasında bir seçim yapmak, bazen karmaşık bir iş olabilir. Bu makalede, Docker Swarm ve Kubernetes'i karşılaştırarak hangi senaryolarda hangi çözümün daha iyi olduğunu anlayacaksınız.
1.  Docker Swarm Nedir?

	Konteyner orkestrasyonu dünyasına ilk adımı atarken, Docker Swarm'ı anlamak iyi bir başlangıç noktası olabilir. Docker Swarm, Docker tarafından geliştirilen, konteyner uygulamalarınızı kolayca yönetmenizi ve dağıtmanızı sağlayan bir konteyner orkestrasyon aracıdır. 


*  Temel Kavramlar:

	Docker Swarm, "Swarm" adını verilen bir grup Docker ana bilgisayarının oluşturulduğu bir yapı üzerinde çalışır. Bu Swarm, konteynerlarınızın dağıtımını, ölçeklenmesini ve yönetimini kolaylaştırır.
	Swarm, yönetim düğümleri (manager nodes) ve çalışma düğümleri (worker nodes) olarak iki temel türde düğüme dayanır. Yönetim düğümleri, Swarm'ın kontrolünü sağlar ve iş yüklerini çalıştıran düğümlere yönlendirir. Çalışma düğümleri, uygulama konteynerlarının çalıştığı düğümlerdir.


* Kolay Kurulum ve Yönetim:

	Docker Swarm, kurulumu ve yapılandırması oldukça basit olan bir araçtır. Bir Docker ana bilgisayarına Docker Swarm modunu etkinleştirerek veya Docker Compose kullanarak hızla bir Swarm kümesi oluşturabilirsiniz.
	Docker Swarm, Docker API'yi kullanır ve Docker komutlarına benzer bir şekilde kullanılır, bu da Docker kullanıcıları için öğrenmesi kolaydır.
	```shell
	docker swarm init
	```

* Docker Compose ile Kolay Yönetim:
	Docker Compose kullanarak, Swarm servislerini tanımlayan bir YAML dosyası oluşturabilir ve birkaç komutla tüm Swarm'ı yönetebilirsiniz. Örneğin;
``` yaml
version: '3'
services:
  web:
    image: my-web-app:latest
    ports:
      - "80:80"
  database:
    image: my-database:latest
    environment:
      MYSQL_ROOT_PASSWORD: examplepass
```
	Yukarıdaki Docker Compose dosyası, iki servisi tanımlar: "web" ve "database". "web" servisi, özel bir web uygulaması görüntüsünü kullanır ve port 80 üzerinden erişilebilir hale getirir. "database" servisi, bir MySQL veritabanı sunucusunu temsil eder ve kök parolasını ayarlar.

	Bu Docker Compose dosyasını kullanarak, Swarm kümenizde bu servisleri başlatabilir ve yönetebilirsiniz. Aşağıdaki komutu kullanarak Swarm üzerinde servisleri başlatabilirsiniz:
	```shell
	docker stack deploy -c docker-compose.yml app
	```


* Yüksek Erişilebilirlik:

	Docker Swarm, yüksek erişilebilirlik sağlamak için tasarlanmıştır. Swarm'daki yönetim düğümleri arasında birincil ve ikincil roller atanabilir, bu da birincil düğümün arızalanması durumunda otomatik olarak ikincil düğümün devralmasını sağlar.


*  Otomatik Yük Dengeleme:

	Swarm, gelen trafik yükünü otomatik olarak düğümler arasında dengeler. Bu, uygulamanızın sürekli olarak kullanılabilir olmasını sağlar.


* Hizmet Yönetimi:

	Docker Swarm, "servisler" olarak adlandırılan uygulama bileşenlerini yönetmek için kullanılır. Bu servisler, belirli sayıda çalışma düğümünde çalıştırılabilir ve gerektiğinde otomatik olarak yeniden başlatılabilir. Örneğin;
```yaml
version: '3'
services:
	web:
		image: e-commerce-web:latest
		ports:
			- "80:80"
	payment:
		image: payment-service:latest
	product:
		image: product-service:latest
	database:
		image: e-commerce-db:latest
		environment:
			MYSQL_ROOT_PASSWORD: mysecretpassword
```
	Yukarıdaki örnek Docker Compose dosyası, bir e-ticaret uygulamasını oluşturur. "web" servisi, kullanıcıların uygulamaya erişebileceği bir web sunucusunu temsil eder. "payment" ve "product" servisleri, ödeme işlemleri ve ürün hizmeti gibi işlevleri yerine getirir. "database" servisi ise veritabanını temsil eder.


2.  Kubernetes Nedir?

	Kubernetes, konteyner orkestrasyonunun açık kaynaklı ve popüler bir platformudur. Google tarafından geliştirilen Kubernetes, karmaşık uygulamaları kolayca dağıtmak, ölçeklemek ve yönetmek için kullanılır. İşte Kubernetes'in temel kavramları ve özellikleri:

* Temel Kavramlar:

	Pods (Kapsüller): Kubernetes'te çalışan en küçük ünite pod'dur. Bir pod, bir veya birden fazla konteyneri içerebilir ve bu konteynerler aynı ağ ve depolama kaynaklarını paylaşırlar.

	Node (Düğüm): Kubernetes kümesinin fiziksel veya sanal makineleri olarak düşünülebilir. Her bir düğüm, Kubernetes tarafından yönetilen konteynerlerin çalıştığı bir sunucuyu temsil eder.

* Dağıtım ve Yönetim:

	Kubernetes, uygulamalarınızın yüksek erişilebilirlik ve hızlı ölçeklenme ile çalışmasını sağlar. Konteyner uygulamalarınızı otomatik olarak düğümler arasında dağıtabilir ve isteğe bağlı olarak yeni konteynerler ekleyebilir veya kaldırabilir.

	Kaynak tahsisi ve otomatik ölçeklendirme, Kubernetes'in en önemli özelliklerinden biridir. Uygulamanızın taleplerine göre kaynakları dinamik olarak ayarlar.

* Servisler ve Yük Dengeleme:

	Kubernetes, servisler adı verilen mantıksal grupları kullanarak konteynerlere erişimi düzenler. Bu, örneğin, bir web uygulamasının ön yüzeyi ve veritabanı hizmeti gibi farklı parçalarını bir araya getirmek için kullanılır.

	Servisler, uygulamanızın sürekli çalışabilirliğini sağlamak için yük dengelemesi yapar. Trafik, servisler aracılığıyla otomatik olarak konteynerlere yönlendirilir.
	Örneğin, "web-app-service" adlı bir servis, "web-app" adlı bir Deployment ile ilişkilendirilebilir:

	```yaml
	apiVersion: v1
	kind: Service
	metadata:
		name: web-app-service
	spec:
		selector:
			app: web-app
		ports:
			- protocol: TCP
				port: 80
				targetPort: 80
		type: LoadBalancer
	```


* Geniş Topluluk ve Ekosistem:

	Kubernetes, büyük bir açık kaynak topluluğu tarafından desteklenir ve sürekli olarak geliştirilir. Bu, yeni özelliklerin ve güncellemelerin hızla uygulanmasını sağlar.

	Kubernetes ekosistemi, bir dizi eklenti ve araç içerir. Bu araçlar, depolama yönetimi, ağ politikaları, izleme, güvenlik ve daha fazlası gibi ek işlevselliği sağlamak için kullanılabilir.

	Bölüm 3: Docker Swarm vs. Kubernetes Karşılaştırması



| Özellikler                | Docker Swarm          | Kubernetes            |
|---------------------------|-----------------------|-----------------------|
| Kolaylık ve Basitlik     | Kolay kurulum ve yapılandırma. Docker ile benzer komutlar. | Daha karmaşık yapı ve daha fazla yapılandırma. |
| Ölçeklenebilirlik         | Küçük ve orta ölçekli  projeler için uygundur ancak büyük projelerde sınırlamaları olabilir. | Küçükten büyüğe  her tür projeyi  kolayca ölçekler.     |
| Topluluk Desteği          | Küçük topluluğa sahip  ve daha az eklenti.  | Geniş ve aktif bir topluluğa sahip.|
| Karmaşıklık               | Basit projeler için uygundur, ancak büyük projelerde bazı eksiklikleri olabilir | Büyük ve karmaşık projeler için tasarlanmış . |
| İşbirliği ve Entegrasyon  | Docker ile entegrasyon avantajlıdır. Docker Compose dosyalarını kullanarak kolayca yönetilebilir. | Birçok entegrasyon ve eklenti sunar. Özellikle büyük ölçekli projeler için işbirliği ve  entegrasyon sağlar. |
|Tavisye Edilen Node Sayısı | 7 | 5000|



4. Hangi Senaryoda Hangi Çözümü Seçmelisiniz?

	Docker Swarm ve Kubernetes, konteyner orkestrasyon dünyasında farklı güçlü yönler sunar. İşte hangi senaryoda hangi çözümü tercih etmeniz gerektiğini belirlemek için dikkate almanız gereken faktörler:

* Küçük ve Basit Projeler:

	Docker Swarm: Küçük bloglar, kişisel projeler veya küçük işletmeler için Docker Swarm ideal bir çözümdür. Basit yapılandırma ve kolay kullanım, bu tür projelerde avantaj sağlar.


* Büyük ve Karmaşık Projeler:

	Kubernetes: Büyük kurumsal projeler, büyük ölçekli e-ticaret siteleri veya karmaşık mikro servis tabanlı uygulamalar için Kubernetes daha uygundur. Ölçeklenebilirlik, karmaşıklık ve çoklu iş yükleri yönetimi için Kubernetes önemli avantajlar sunar.


* Docker İle Uyum:

	Docker Swarm: Docker teknolojileri ile derin bir entegrasyon istiyorsanız Docker Swarm tercih edilebilir. Docker Compose dosyalarını doğrudan kullanabilirsiniz.


* Büyük Topluluk ve Eklenti Desteği:

	Kubernetes: Geniş bir topluluk ve birçok üçüncü taraf eklentisi ile çalışmak istiyorsanız Kubernetes ideal bir seçenektir. Bu, projenizin büyümesine ve ihtiyaçlarınıza uygun özellikler eklemeye olanak tanır.


* Otomatik Ölçeklendirme ve Yük Dengeleme:

	Kubernetes: Otomatik ölçeklendirme ve gelişmiş yük dengeleme özellikleri gerekiyorsa, Kubernetes bu ihtiyaçları karşılayabilir. Büyük trafiği etkili bir şekilde yönlendirmek için yararlıdır.


* Karmaşıklık ve Yapılandırma:

	Docker Swarm: Projelerinizin karmaşıklığı düşükse ve hızlı bir şekilde başlamak istiyorsanız, Docker Swarm daha az yapılandırma ve karmaşıklık sunar.


Sonuç

Docker Swarm ve Kubernetes, konteyner orkestrasyonu için iki önde gelen platformdur ve her biri kendi avantajlarına sahiptir. Hangi platformu seçeceğiniz, projenizin ihtiyaçlarına ve büyüklüğüne bağlıdır. İşte bu makalede ele aldığımız bazı anahtar noktalar:

Docker Swarm, küçük ve basit projeler için idealdir. Docker ile entegrasyonu kolaydır ve kullanımı basittir. Küçük uygulamalar, kişisel projeler ve basit bloglar için Docker Swarm hızlı bir başlangıç yapmanın mükemmel bir yoludur.

Kubernetes, büyük ve karmaşık projeleri destekler. Büyük kurumsal uygulamalar, büyük ölçekli e-ticaret siteleri ve çoklu iş yükleri yönetimi gereken projeler için uygundur. Geniş topluluk ve üçüncü taraf eklentileri sayesinde çok yönlü bir platform sunar.


Son Düşünceler:
Projelerinizi ve ihtiyaçlarınızı değerlendirmek, hangi çözümün sizin için daha uygun olduğunu belirlemek için önemlidir.Her iki platform da konteyner orkestrasyonunda büyük adımlar atmıştır ve ihtiyaçlarınıza göre seçiminizi yaparken bu faktörleri göz önünde bulundurmanızı öneririm.

Kaynaklar;

[Docker Swarm Official Guide](https://docs.docker.com/engine/swarm/)

[Docker Swarm Nodes](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)

[Kubernetes Overview](https://kubernetes.io/docs/concepts/overview/)

[Kubernetes and Docker freeCodeCamp](https://www.freecodecamp.org/news/kubernetes-vs-docker-swarm-what-is-the-difference/)
