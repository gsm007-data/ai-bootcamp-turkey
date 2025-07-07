# 🥇 İş Otomasyonu - Rekabetçi Görüşler

![image](assets/hypercar3.png)


## 🤔 Problem

ABC Motors Corp'un satış departmanı, yeni yüksek performanslı araç serisi için satış teklifleri hazırlama konusunda zorluklarla karşılaştı. Her yeni model çıkardıklarında, rekabetçi analiz ekibi görüşlerini sunmak için çok fazla zaman ve kaynak harcıyor. Sorunlar şunları içeriyor:

- Manuel araştırma kararları geciktirir ve üretkenliği azaltır.

- Zayıf konumlandırma satış farklılaştırmasını engeller.

- Gerçek zamanlı istihbarat olmadan pazar değişikliklerine yavaş yanıt.

## 🎯 Amaç

ABC Motors Corp, pazar araştırması ve rakip analizini otomatikleştirmek için AI destekli bir Rekabetçi İstihbarat Sistemi uygulamayı planlıyor. Bu sistem, satış ekiplerinin ürünlerini rakiplere karşı hızla tanımlamasına ve konumlandırmasına yardımcı olacak, manuel araştırmanın verimsizliklerini ve güncel olmayan görüşleri aşacak. Amaç, rekabetçi analiz ve pazar araştırmasını destekleyen AI destekli bir sistem oluşturmak:

* Şirketin ürün kataloğundan ürünleri çıkarmak.
* Her ürünün temel özelliklerini tanımlamak ve çıkarmak.
* Temel özellikler temelinde rakip ürünleri aramak.
* Fiyat, özellikler ve farklılaştırıcılarla yapılandırılmış rekabetçi karşılaştırma tablosu oluşturmak.
* Daha derin stratejik görüşler sağlamak için SWOT Analizi (Güçlü Yönler, Zayıf Yönler, Fırsatlar ve Tehditler) gerçekleştirmek.

Bu görevleri otomatikleştirerek, şirket satış süreçlerini hızlandırmayı, veri doğruluğunu artırmayı ve satış ekiplerinin daha hızlı bilinçli kararlar almasını sağlamayı hedefliyor.

## 📈 İş Değeri

* Manuel rakip araştırma zamanında azalma.
* Pazar rekabeti hakkında otomatik, gerçek zamanlı güncellemeler.
* Geliştirilmiş satış sunumu etkinliği

## 🏛 Mimari

Rekabetçi analiz sürecini kolaylaştırmak için, [ABC Motors Corp'un Ürün Kataloğu](assets/ABC_Motor_Product_Catalog.pdf)'ndan ürün verilerini özerk olarak çıkaran ve analiz eden bir Çok Ajanlı AI Otomasyon Sistemi tasarladık. Bu sistem, satış ve strateji ekipleri için verimlilik, doğruluk ve gerçek zamanlı görüşler sağlayan işbirlikçi çok ajanlı bir yaklaşım kullanır. Mimari, temel işlevleri yerine getirmek için birlikte çalışan özel AI ajanlarından oluşur:
  * Ürün kataloğundan ürünleri çıkarmak
  * Ürün kataloğundan ürünün özelliklerini çıkarmak,
  * Rakip ürünleri aramak
  * Yapılandırılmış rekabetçi karşılaştırma tablosu oluşturmak
  * Güçlü Yönler, Zayıf Yönler, Fırsatlar ve Tehditler (SWOT) Analizi

Bu sistem, rekabetçi araştırmayı otomatikleştirmek, satış sunumlarını güçlendirmek ve manuel çabayı en aza indirmek için sorunsuz bir şekilde birlikte çalışan watsonx Orchestrate ajanı ve watsonx.ai ajanının birleşik gücünden yararlanır.

<img width="900" alt="image" src="assets/Business_Automation_Architecture.png">

Bu kullanım durumu, ürün kataloğundan ürüne özel bilgileri (isimler ve özellikler gibi) çıkarmak ve ürün karşılaştırmaları yapmak için watsonx Orchestrate ajanının yeteneklerini kullanır. Bu ajanlar, watsonx.ai Agent Lab'da geliştirilen özel bir ajan tarafından desteklenir ve tümü watsonx Orchestrate içinde entegre edilir. watsonx Orchestrate sohbet asistanı aracılığıyla, ajanlar sorunsuz bir şekilde işbirliği yapar ve görevleri devrededer, kapsamlı görüşler sunar ve bilinçli karar vermeyi sağlar.

  * **Product Agent** : Bu ajan, tüm sorgular için giriş noktası olarak hizmet eder ve belirli bir ürünü aramak, ürün kataloğundan detaylarını ve özelliklerini yapılandırılmış bir formatta almak için tasarlanmıştır. Temel ürün bilgilerini sistematik olarak sunarak anlaşılması ve kullanılması kolay hale getirerek netlik ve organizasyon sağlar. Ayrıca, daha fazla işlem için görevleri Comparison Agent'a devreder.

  * **Comparison Agent** : Bu ajan, ürün karşılaştırmasının uçtan uca sürecini ele alır. Önce eşleşen özellikler temelinde benzer ürünler için URL'leri tanımlar ve toplar. Ardından, bu bağlantıları kullanarak rakip tekliflerini analiz eder, temel görüşleri çıkarır ve her ürün için detaylı SWOT analizi oluşturur. Bulgular, hızlı ve etkili karşılaştırma sağlamak için net, yapılandırılmış tablo formatında sunulur.

## 📝 Adım Adım Uygulamalı Laboratuvar
Adım adım talimatları burada bulabilirsiniz:

[Adım adım uygulamalı kılavuz](./hands-on-lab-buisness-automation.md)

## Demo Video
Çözümün video demosu aşağıdadır:

<video width="800" controls>
  <source src="./video/solution.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

[Videoya doğrudan bağlantı](https://raw.githubusercontent.com/gsm007-data/ai-bootcamp-turkey/tr_gsm/usecases/business-automation/video/solution.mov)