# 🥇 Financial Analyst Agent

<img width="900" alt="image" src="images/blue_aurum_img.png">

## 🤔 Problem

Blue Aurum Financial, hissedarlarına daha fazla değer sunmak için yatırımlarını genişletmek ve ölçeklendirmek istiyor. Ancak, finansal araştırma analisti ekibi, potansiyel yeni yatırım fırsatları için araştırma ve durum tespiti yapma sürecinin uzun sürmesi nedeniyle yeni yatırım fırsatlarını hızla belirlemekte zorlanıyor.

Takip ettikleri süreç çoğunlukla manuel olup, finansal araştırma analistinin ilgilendiği bir kuruluş için finansal raporları incelemesini ve aynı sektördeki diğer kuruluşlarla veya Blue Aurum Financial'ın zaten yatırım yaptığı kuruluşlarla karşılaştırmasını gerektiriyor. Karşılaştırmalı bir özet oluşturduktan sonra, finansal araştırma analisti şirket, yönetim ekibi, son analist raporları ve son haberler hakkında ayrıntılı bilgi almak için çevrimiçi arama yaparak perspektifini geliştirmeye çalışır. Ayrıca potansiyel getirileri tahmin etmek için dahili finansal modelleme araçlarından yararlanabilir.

Özetle, Blue Aurum Financial'daki finansal araştırma analistlerinin karşılaştığı zorluklardan bazıları şunlardır:

- Manuel araştırma, yeni yatırım fırsatlarının belirlenmesinde gecikmelere yol açar.

- Araştırma, tahmin modellemesi için dahili araçlarla çalışmayı, kamu verileri karşısında harici arama yapmayı ve önemli manuel çaba gerektiren finansal raporları incelemeyi/analiz etmeyi içerir.

- Piyasa volatilitesi ve yatırımcı/analist duyarlılığındaki değişiklik, finansal araştırma analistlerinin incelemelerini, bulgularını ve önerilerini sürekli olarak yeniden değerlendirmesini gerektirir.

## 🎯 Amaç

Blue Aurum Financial, finansal araştırma analisti ekibini araştırmalarını hızlandırmada ve yüksek değerli yatırım fırsatları üretmede desteklemek için AI destekli bir Financial Research Agent uygulamayı planlamaktadır. Amaç, finansal araştırma analistlerini aşağıdaki görevleri yerine getirmede destekleyen AI destekli agentic çözümler oluşturmaktır:

* Finansal raporları ayrıştırır ve önemli bilgileri çıkarır.
* Finansal raporlarına dayalı olarak farklı kuruluşlar arasında karşılaştırmalı analiz sağlar.
* Bir kuruluş hakkında ayrıntılı bilgilerin yanı sıra son haberler ve analist raporları için kamu bilgilerini arar.
* API'ler aracılığıyla finansal metrikleri alma için dahili araçları çalıştırır.
* Bulguların ve analizin bir raporunu oluşturur.

Bu görevleri otomatikleştirerek şirket, yatırım için yeni fırsatları belirlemek amacıyla araştırma sürecini hızlandırmayı hedeflemektedir.

## 📈 İş Değeri

* Manuel araştırma süresinde azalma.
* Son haberler, piyasa verileri ve analist raporları dahil olmak üzere piyasa bilgileri hakkında otomatik, gerçek zamanlı güncellemeler.
* Durum tespiti ve otomatik araştırmaya dayalı geliştirilmiş öneriler.

## 🏛 Mimari

Araştırma sürecini kolaylaştırmak için Blue Aurum Financial, [watsonx Orchestrate](https://www.ibm.com/products/watsonx-orchestrate) ile desteklenen Multi-Agent Financial Research çözümü tasarlamak için IBM ile ortaklık kurdu. Aşağıdaki mimari, görevlerini yerine getirirken kullandıkları araçların yanı sıra dahil olan çeşitli AI agentlerini göstermektedir.

Mimari, temel işlevleri gerçekleştirmek için birlikte çalışan özel AI agentlerden oluşur:
  * Web Search Agent, web arama sorgularını yürütme ve güncel bilgileri alma konusunda yetenekli. Web Search Agent, DuckDuckGo ve Brave gibi birden fazla arama aracı kullanarak kamu bilgileri için web araması yapmak ve tutarlı, eksiksiz bir yanıt sunmak için sonuçları toplamak üzere tasarlanmıştır.
  * Financial API Agent, Glossary Tool (belirli finansal terimleri açıklamak için) ve son piyasa verilerini döndüren Market Data Tool kullanarak bilgi alma konusunda yetenekli. Bu bootcamp'te, agentin piyasa verilerini almak için bu aracı nasıl kullanabileceğini göstermek için Market Data Tool'u kullanıyoruz. Pratikte, benzer şekilde eklenebilecek diğer araçlar, finansal araştırma analistlerinin bir varlığın performansını modelleyebilmesi için API aracılığıyla sunulan dahili modelleme araçlarını temsil edebilir.
  * Financial Analyst Agent, finansal araştırma analistlerinden gelen sorulara yanıt veren ana orkestratör agent. Giriş sorgusuna dayalı olarak akıl yürütebilen ve en iyi nasıl yanıt vereceğine karar verebilen akıllı bir agent. RAG (Retrieval Augmented Generation) modelini etkinleştiren sorulara yanıt vermek için dahili bir bilgi tabanından yararlanabilir veya kullanıcı sorgularını en iyi şekilde ele almak için diğer agentlerden birine yetki devredebilir.

Bu sistem, IBM'in agentic AI çözümleri geliştirmek için no-code/low-code/pro-code ürünü olan [watsonx Orchestrate](https://www.ibm.com/products/watsonx-orchestrate) ve IBM'in Large Language Models (LLMs) gibi temel modelleri barındırmak için platformu olan [watsonx.ai](https://www.ibm.com/products/watsonx-ai)'nin gücünden yararlanır.

<img width="900" alt="image" src="images/banking-fra-architecture.png">

Özetle, bu bootcamp'te finansal araştırmayı hızlandırmaya yardımcı olmak için financial research agent geliştirmek amacıyla birden fazla agent ve ilgili araçlar geliştirmek için watsonx Orchestrate'in yeteneklerini nasıl kullanacağınızı öğreneceksiniz. Agent, bilgi belgelerini (kazanç raporları gibi) anlama, karşılaştırmalı analiz yapma, son haberler için web'de arama yapma ve piyasa verilerini alma konusunda yetenekli olup, finansal araştırma analistlerinin yatırım önerileri yapmak için ilgili bilgileri hızla bulmasına yardımcı olur.

## 📝 Adım Adım Uygulamalı Laboratuvar
Adım adım talimatları burada bulabilirsiniz:

[Adım adım uygulamalı kılavuz](https://github.ibm.com/skol/agentic-ai-client-bootcamp/blob/staging/usecases/banking-financial-research-analyst/hands-on-lab-banking.md)

## Demo Video
Çözümün demo videosu aşağıdadır:

https://github.ibm.com/skol/agentic-ai-client-bootcamp/assets/3814/b8dcddde-9187-4a12-ba8f-9271573a0c30