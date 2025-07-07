# 👨🏻‍💻 Kullanım Durumu: Financial Analyst Agent  

## İçindekiler
- [Kullanım Durumu Açıklaması](#kullanım-durumu-açıklaması)
- [Mimari](#mimari)
- [Ön Koşullar](#ön-koşullar)
- [watsonx Orchestrate](#watsonx-orchestrate)
  - [watsonx Orchestrate'e Erişim](#watsonx-orchestratee-erişim)
- [Financial Analyst Agent Oluşturma](#financial-analyst-agent-oluşturma)
  - [Bilgi Tabanı ile Agent Yapılandırması](#bilgi-tabanı-ile-agent-yapılandırması)
- [Financial API Agent Oluşturma ve Yapılandırması](#financial-api-agent-oluşturma-ve-yapılandırması)
- [Web Search Agent Oluşturma ve Yapılandırması](#web-search-agent-oluşturma-ve-yapılandırması)
- [Bir Araya Getirme - Tam Agent İşbirliği](#bir-araya-getirme)
- [watsonx Orchestrate Sohbet Arayüzü ile Agentları Deneyimleme](#watsonx-orchestrate-sohbet-arayüzü-ile-agentları-deneyimleme)
- [Sonuç](#sonuç)

## Kullanım Durumu Açıklaması

Blue Aurum Financial, finansal araştırma analistleri ekibini araştırmalarını hızlandırmada ve yüksek değerli yatırım fırsatları üretmede desteklemek için AI destekli bir Financial Research Agent uygulamayı planlıyor. Amaç, finansal araştırma analistlerinin aşağıdaki görevleri yerine getirmesinde onlara destek olan AI destekli ajantik çözümler oluşturmaktır:

* Finansal raporları ayrıştırır ve anahtar bilgileri çıkarır.
* Finansal raporlarına dayalı farklı varlıklar arasında karşılaştırmalı analiz sağlar.
* Bir varlık hakkında ayrıntılar ile son haberler ve analist raporları için genel bilgileri arar.
* API'ler aracılığıyla finansal metrikleri almak için dahili araçları yürütür.
* Bulgular ve analizin raporunu oluşturur.

Bu görevleri otomatikleştirerek, şirket yatırım için yeni fırsatları belirlemek amacıyla araştırma sürecini hızlandırmayı amaçlıyor.

## 🏛 Mimari  <a id="mimari"></a>

<img width="900" alt="image" src="images/banking-fra-architecture.png">

## Ön Koşullar
Bu bootcamp'in uygulamalı laboratuvar bölümündeki adımları çalıştırmak için, bu bootcamp'in hazırlığının bir parçası olarak sizin için sağlanan **watsonx Orchestrate** ve **watsonx.ai**'ye erişiminiz olması gerekir.

- API anahtarı oluşturma ve proje kurulumu adımları için [environment-setup](https://github.ibm.com/skol/agentic-ai-client-bootcamp/tree/staging/environment-setup) kılavuzunu inceleyin.

- Devam etmeden önce **tüm sistemlerin** çalışır durumda olduğundan emin olmak için eğitmeninizle kontrol edin.

## watsonx Orchestrate
[Çözüm Mimarisi](images/banking-fra-architecture.png)'nde detaylandırıldığı gibi, çözüm için agentların çoğunu watsonx Orchestrate'de oluşturacak ve dağıtacağız. AI Agentları, görevleri çalıştırabilen, karar verebilen ve çevreleriyle etkileşim kurabilen özerk varlıklardır. IBM watsonx Orchestrate'de agentlar, değişen koşullara uyum sağlayabilen ve yanıt verebilen karmaşık, dinamik sistemlerin oluşturulmasını sağlayan önemli bir bileşendir.

### watsonx Orchestrate'e Erişim
watsonx Orchestrate'e erişmek için şu adımları izleyin:

1- IBM Cloud hesabınıza henüz giriş yapmadıysanız, tercih ettiğiniz tarayıcıda https://cloud.ibm.com adresine gidin ve kimlik bilgilerinizle (TechZone rezervasyonunuz için kullandığınız) giriş yapın.

2- IBM Cloud ana sayfanızda, sol üst navigasyon menüsüne (hamburger menü) tıklayın ve **Kaynak listesi**'ni seçin (kırmızı dikdörtgenle belirtilmiş).
*Not: Birden fazla IBM Cloud hesabının üyesiyseniz, [environment-setup](https://github.ibm.com/skol/agentic-ai-client-bootcamp/tree/staging/environment-setup) kılavuzunda açıklandığı gibi gerekli hizmetlerin mevcut olduğu doğru hesapta (kırmızı oval ile belirtilmiş) çalıştığınızdan emin olun.*
![IBM Cloud Resource List](images/ibm_cloud_resources.png) 

3- Kaynak Listesi sayfasında, **AI / Machine Learning** bölümünü genişletin (kırmızı okla belirtilmiş) ve **Watsonx Orchestrate** hizmetinin (kırmızı dikdörtgenle belirtilmiş) hizmet adına tıklayın.
![IBM Cloud wxo](images/ibm_cloud_wxo.png) 

4- Hizmeti başlatmak için **Launch watsonx Orchestrate** (kırmızı okla belirtilmiş) düğmesine tıklayın.
![wxo launch](images/wxo-launch.png) 

5- watsonx Orchestrate hizmeti başlatıldıktan sonra, aşağıdaki şekilde gösterilen ana sayfasında olacaksınız. watsonx Orchestrate ile etkileşim kurmaya başlamak için herhangi bir metin yazabileceğiniz bir sohbet alanı (kırmızı dikdörtgenle belirtilmiş) ile sezgisel bir konuşma arayüzü göreceksiniz. Yeni bir hizmet örneği ile başladığınızda, hiçbir özel agent tanımlanmamış olacak ve bu nedenle **Agents** altındaki bölüm *No agents available* şeklinde görünecektir. **Agents** bölümünde **Create or Deploy** bir agent'a tıklayabilir veya yeni agentlar geliştirmeye başlamak için **Create new agent** (kırmızı okla belirtilmiş) düğmesine tıklayabilirsiniz. Agent yönetimi sayfasına gitmek için **Manage agents** bağlantısını da seçebilirsiniz.
Birkaç genel soru sormayı deneyin ve özel agentlar oluşturulana kadar temel işlevselliği sağlayan watsonx Orchestrate'deki önceden oluşturulmuş agenti destekleyen büyük dil modelinden (LLM) gelen yanıtları gözlemleyin.
![wxo landing page](images/wxo-landing-page.png) 

## Financial Analyst Agent Oluşturma
Bu bölümde, watsonx Orchestrate'de bir AI agent oluşturma sürecini inceleyeceksiniz:

6- Agentlar oluşturmaya başlamak için, 5. adımda belirtildiği gibi **Create new agent** bağlantısına tıklayabilir veya alternatif olarak, sol üst navigasyon menüsüne tıklayıp **Build** bölümünü (kırmızı okla belirtilmiş) genişletebilir ve **Agent Builder**'ı (kırmızı dikdörtgenle belirtilmiş) seçebilirsiniz. Bu sizi Manage agents sayfasına yönlendirecektir.
![wxo agent builder](images/wxo-nav-menu-agent-builder.png) 

7- Manage agents sayfası başlangıçta boş olacaktır çünkü henüz hiçbir agent oluşturulmamıştır. Akıl yürütebilen ve eylem yapabilen daha fazla AI agent oluşturdukça, Manage agents sayfası bu agentlarla doldurulacaktır. İlk agentınızı oluşturmaya başlamak için **Create agent** düğmesine (kırmızı okla belirtilmiş) tıklayın.
![wxo create agent](images/wxo-create-agent-manage-agents-empty.png) 

8- Create an agent sayfasında, **Create from scratch** kartını (kırmızı dikdörtgenle belirtilmiş) seçin, agent için bir **Name** ve **Description** sağlayın ve **Create** (kırmızı okla belirtilmiş) düğmesine tıklayın.

Name: 
```
Financial Analyst Agent
```

Description: 
```
Agent skilled at financial research using internal knowledge and external search of public information.
```
Bir agentin doğal dil açıklaması önemlidir çünkü ajantik çözüm tarafından kullanıcı mesajlarını isteği ele almada yetenekli olan doğru agente yönlendirmek için kullanılır. Daha fazla ayrıntı için lütfen [Understanding the description attribute for AI Agent](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-creating#understanding-the-description-attribute-for-ai-agent) dokümantasyonunu inceleyin.

watsonx Orchestrate, sıfırdan agent oluşturmayı veya şablondan oluşturmayı destekler, bu da mevcut agentların bir kataloğuna göz atmayı ve başka bir agentin özelliklerini yeni agent için şablon olarak kullanmayı içerir. Bu laboratuvar için, sıfırdan agentlar oluşturacaksınız.

*Not: AI agentlarının nasıl çalıştığı konusunda biraz geçmiş bilgi için [What are AI Agents?](https://www.ibm.com/think/topics/ai-agents) bloğunu incelemeniz önerilir.*
![wxo financial analyst agent](images/wxo-financial-analyst-agent.png) 

### Bilgi Tabanı ile Agent Yapılandırması
AI Agent oluşturulduktan sonra, bu bölümde agenti bilgi tabanından gelen bilgileri kullanarak sorulara yanıt vermesini ve araçları kullanarak görevleri gerçekleştirmesini sağlamak için bilgi ve araçlarla yapılandırma sürecini inceleyeceksiniz.

9- Sonra, agentınızı yapılandırma sürecini inceleyeceksiniz. Financial Research Agent sayfası iki yarıya bölünmüştür. Sağ yarı, agentınızın davranışını test etmenize olanak tanıyan bir **Preview** (kırmızı oval ile belirtilmiş) sohbet arayüzüdür. Sayfanın sol yarısı, agentınızı yapılandırmak için kullanabileceğiniz dört anahtar bölümden (kırmızı dikdörtgenlerle belirtilmiş) oluşur.

   - Profile: **Profile** bölümü, agenti oluştururken sağladığınız agentin açıklamasından oluşur. Gerektiğinde agentin açıklamasını düzenlemek ve geliştirmek için her zaman bu bölüme gidebilirsiniz.

   - Knowledge: **Knowledge** bölümü, agente bilgi eklediğiniz yerdir. Agentlere bilgi eklemek, belirli kullanım durumları için doğru ve bağlamsal olarak ilgili yanıtlar üretmek amacıyla gerekli bilgileri sağlayarak konuşma yeteneklerini geliştirmede önemli bir rol oynar. Doğrudan agente dosyalar yükleyebilir veya içerik deposu olarak bir Milvus veya Elasticsearch örneğine bağlanabilirsiniz. Bu **Knowledge** arayüzü sayesinde, AI agentlerinizin kurumsal bilgi tabanı gibi güvenilir bir veri kaynağına dayalı yanıtları temellendirmek için çok popüler bir AI deseni olan Retrieval Augmented Generation (RAG) desenini uygulamasını sağlayabilirsiniz.
   
   *Not: Daha fazla ayrıntı için [Adding knowledge to agents](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-knowledge) dokümantasyonunu inceleyin.*

   - Toolset: *Knowledge* agentleri güvenilir bir bilgi tabanı ile güçlendirme yönteminizken, **Toolset** agentleri *Tools* ve *Agents* sağlayarak eylem almalarını sağlamanın yoludur. Agentler **Tools** kullanarak görevleri tamamlayabilir veya bu tür görevlerde derinlemesine yetenekli olan diğer **Agents**'a görevleri devredebilir.

   *Not: Daha fazla ayrıntı için dokümantasyonun [Adding tools to an agent](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-tools) ve [Adding agents for orchestration](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-orchestration) bölümlerini inceleyin.*
   
   - Behavior: Agent yapılandırmasının **Behavior** bölümü, agentin kullanıcı isteklerine ve durumlara nasıl yanıt verdiğini tanımlamak için talimatlara sağladığınız yerdir. Agentin ne zaman ve nasıl eylem alması gerektiğini belirleyen kurallar yapılandırabilirsiniz. Bu kurallar, agentin öngörülebilir ve tutarlı bir şekilde davranmasına yardımcı olur ve kesintisiz bir kullanıcı deneyimi sunar.

   *Not: Daha fazla ayrıntı için [Adding instructions to agents](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-instructions) dokümantasyonunu inceleyin.

Son olarak, agent yapılandırmanızı tamamladıktan ve performansını test ettikten sonra, agenti seçilen kanal üzerinden kullanılabilir hale getirmek için **Deploy** (kırmızı okla belirtilmiş) edebilirsiniz. Şu anda desteklenen ana kanal, watsonx Orchestrate'i ilk başlattığınızda eriştiğiniz *Chat* ana sayfasıdır. Ürün, agentınızı dağıtabileceğiniz ek kanallar için destek ekleyecektir.

![wxo create agent config](images/wxo-create-agent-config.png) 

10- Agent yapılandırma sayfasında, **Profile** bölümündeki agentin *Description*'ını gözden geçirin ve olduğu gibi bırakın (düzenleme gerekmez). Sonra, **Knowledge** bölümüne kaydırın veya **Knowledge** kısayoluna (kırmızı oval ile belirtilmiş) tıklayın. Knowledge bölümünde, agenti bilgi içeriği hakkında bilgilendirmek için bir açıklama ekleyin. Bu laboratuvar için, bir avuç şirket için birkaç son kazanç raporu sağlayacağımız için aşağıdaki açıklamayı ekleyin.

Description: 
```
This knowledge addresses all details about earning reports for the companies of interest. Research analysts can ask about any details from earning reports.
```

Sonra, agente bilgi sağlama yöntemini seçmeniz gerekir. watsonx Orchestrate, agente bilgi eklemeyi ya UI üzerinden dosyaları doğrudan yükleyerek ya da bir içerik deposuna (Mivlus veya ElasticSearch) işaret ederek destekler. [Adding knowledge to agents](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-knowledge) dokümantasyonu daha fazla ayrıntı sağlar. Bu laboratuvar için, AMZN, META, NVDA ve NFLX için kazanç raporlarını yakalayan pdf dosyalarını yüklemek için **Upload files** düğmesine (kırmızı okla belirtilmiş) tıklayın.

![wxo agent config knowledge](images/wxo-agent-config-knowledge.png) 

Agent için bilgiye yüklemek üzere aşağıdaki pdf dosyalarını sürükleyip bırakın:
   - [AMZN-Q4-2024-Earnings.pdf](documents/AMZN-Q4-2024-Earnings.pdf)
   - [META-Q4-2024-Earnings.pdf](documents/META-Q4-2024-Earnings.pdf)
   - [NFLX-Q4-2024-Earnings.pdf](documents/NFLX-Q4-2024-Earnings.pdf)
   - [NVDA-Q4-2024-Earnings.pdf](documents/NVDA-Q4-2024-Earnings.pdf)

![wxo knowledge upload files](images/wxo-knowledge-upload-files.png) 

11- Dosyalar bilgi tabanına yüklendikten sonra, agentin bu bilgi tabanını kullanarak sorulara nasıl yanıt verebileceğini doğrulamak için agenti test etmeye başlayabilirsiniz. Yüklenen dosyalar işlenir ve agent tarafından kullanılmak üzere hazırlanır. Yükleme tamamlandıktan sonra, şu gibi birkaç soru sorarak agenti test edin:

```Can you tell me about Meta's business```

```I'm interested in learning more about Meta and Amazon. Can you tell me a bit about their businesses?```

Yanıtların yüklenen belgelerden alındığını ve sonra agentin ürettiği nihai yanıtı aşağıdaki şekilde gösterildiği gibi görmelisiniz.

![wxo agent knowledge test](images/wxo-agent-knowledge-test.png) 

```Give Toyota q4 financial results``` gibi bir test yapmayı deneyin ve agentin yanıtını inceleyin, bu da aşağıdaki şekilde gösterildiği gibi Toyota hakkında bilgisinin olmadığını belirtmeli.

![wxo financial agent knowledge negative](images/wxo-financial-analyst-knowledge-negative-test.png) 

Bu noktada, şu ana kadar geliştirdiğiniz şeyi yansıtmak için bir dakikanızı ayırmaya değer. Bir agent tasarladınız ve onu bağlamında sorulara yanıt vermesini sağlamak için bir bilgi tabanı ile güçlendirdiniz. *Tebrikler!!*

Mimariyi gözden geçirir, Financial Analyst agentini oluşturma ve onu bir bilgi tabanı ile güçlendirme (aşağıdaki şekilde kırmızı dikdörtgenlerle belirtilmiş) ile ilgili ajantik çözümün bölümünü tamamladınız. Sonraki bölümde, daha sonra **Financial Analyst Agent**'a işbirlikçi agentlar olarak ekleyeceğiniz **Financial API Agent** ve **Web Search Agent**'ı oluşturma sürecini inceleyeceksiniz.

![wxo agent knowledge complete](images/wxo-financial-research-agent-knowledge-complete.png) 

## Financial API Agent Oluşturma ve Yapılandırması
Bu bölümde, piyasa verilerini ve sözlük tanımlarını döndürmede özellikle yetenekli olan işbirlikçi agentlerden biri olan Financial API Agent'ı geliştireceksiniz. Bu uygulamalı laboratuvarda, Financial API Agent iki araçla güçlendirilmiştir: hisse senedi fiyatlarını döndüren **Market Data Tool** ve sözlük tanımlarını döndürmek için Wikipedia'yı kullanan **Glossary Tool**. Pratikte, bu agent ayrıca hisse senedi davranışını modelleme veya hisse senedi fiyatlarını tahmin etme gibi diğer dahili araçlara da erişebilir; agenti bu tür araçlarla güçlendirme yaklaşımı aynı olacaktır.

12- watsonx Orchestrate ana sayfasında (sohbet arayüzü) değilseniz, IBM Cloud'a giriş yaptığınızdan emin olmak, watsonx Orchestrate hizmetini bulup ana sayfaya erişmek için başlatmak amacıyla yukarıdaki adımları tekrarlayın.

13- watsonx Orchestrate ana sayfasından, yeni bir agent olan Financial API Agent'ı geliştirmeye başlamak için **Create agent** (kırmızı dikdörtgenle belirtilmiş) düğmesine tıklayın.

![wxo create agent chatUI](images/wxo-create-agent.png) 

14- Create an agent sayfasında, **Create from scratch** kartını seçin, agent için bir **Name** ve **Description** sağlayın ve **Create** (kırmızı okla belirtilmiş) düğmesine tıklayın.

Name: ```Financial API Agent```

Description: 
```
Agent skilled in retrieving market data as well as glossary definitions for financial terms.
```
Daha önce açıklandığı gibi, bir agentin açıklaması önemlidir çünkü ajantik çözüm tarafından kullanıcı mesajlarını isteği ele almada yetenekli olan doğru agente yönlendirmek için kullanılır.

![wxo create financial api agent](images/wxo-create-financial-api-agent.png) 

15- Agent yapılandırma sayfasında, **Toolset** bölümüne kaydırın veya kısayola (kırmızı oval ile belirtilmiş) tıklayın. Sonra agente araç eklemek için pencereyi açmak üzere **Add tool** düğmesine (kırmızı okla belirtilmiş) tıklayın.

![wxo agent tools](images/wxo-agent-tools.png) 

16- Araç seçenekleri pop-up'ında, aşağıdaki şekilde gösterildiği gibi **Import** (kırmızı dikdörtgenle belirtilmiş) seçeneğini seçin.

![wxo tool options](images/wxo-tool-options.png) 

watsonx Orchestrate, [Adding tools to an agent](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=agents-adding-tools) dokümantasyonunda açıklandığı gibi agentlara araç ekleme için birden fazla yaklaşımı destekler:

   - Add from catalog: **Add from catalog** seçeneği, önceden tanımlanmış araçlardan oluşan zengin bir katalogdan bir araç eklemenizi sağlar. Araç katalogu, agentlere araç eklemeyi daha da kolaylaştırmak için aktif olarak geliştirilmektedir.

   - Add from local instance: **Add from local instance** seçeneği, watsonx Orchestrate'in yerel örneğine zaten yüklenmiş mevcut araçlar kümesinden bir araç eklemenizi sağlar.

   - Import: **Import** seçeneği, bir OpenAPI spesifikasyonu kullanarak harici bir araç içe aktarmanızı ve araç olarak hangi operasyonları içe aktarmak istediğinizi seçmenizi sağlar.

   - Create a new flow: **Create a new flow** seçeneği, koşullu kontroller ve aktiviteler kullanan bir adım dizisi oluşturmak için sürükle ve bırak araç oluşturucu arayüzü sağlar.

Ayrıca, belirli bir watsonx Orchestrate örneğine Python ve OpenAPI araçları geliştirmek ve yüklemek için watsonx Orchestrate [Agentic Development Kit (ADK)](https://developer.watson-orchestrate.ibm.com/)'yi kullanabilir, sonra bunları agentlara ekleyebilirsiniz.
watsonx Orchestrate aynı zamanda [Model Context Protocol (MCP)](https://developer.watson-orchestrate.ibm.com/) araçlarının eklenmesini de destekler. Eğer tanımıyorsanız, MCP, AI Agentlerini içerik depoları, iş araçları ve geliştirme ortamları dahil olmak üzere verilerin yaşadığı sistemlere bağlamak için bir standarttır. MCP, agentleri araçlarla güçlendirme standardı olarak giderek daha popüler hale geliyor.

Financial API Agent amaçları için, bir OpenAPI spesifikasyonu içe aktarmak ve araç olarak hangi operasyonları içe aktaracağınızı tanımlamak için **Import** seçeneğini kullanacaksınız. Eğitmeniniz tarafından sağlanacak olan **financial_api_openapi.json** dosyasına ihtiyacınız olacak.

17- Import tool sayfasında, eğitmeniniz tarafından sağlanan **financial_api_openapi.json** dosyasını (kırmızı dikdörtgenle belirtilmiş) sürükleyip bırakın ve **Next** (kırmızı okla belirtilmiş) düğmesine tıklayın.

![wxo tool import openapi](images/wxo-tool-import-openapi.png) 

18- Sonra, **Get Stock Price Data**, **Get Stock Information**, **Get Financial Statements**, **Get Earnings Report**, ve **Search Wikipedia** operasyonları için onay kutularını seçin (kırmızı oklarla belirtilmiş) ve **Done** düğmesine tıklayın.

![wxo tool import operations](images/wxo-tool-import-operations.png) 

19- Bu noktada, Tools alt bölümü altında içe aktarılan araçları göreceksiniz, bu da **Financial API Agent**'ın piyasa verilerini almayı veya sözlük bilgilerini elde etmeyi gerektiren görevleri yürütmede bu araçları kullanabileceği anlamına gelir.

20- Sonra, **Behavior** bölümüne daha fazla kaydırın veya **Behavior** kısayoluna (kırmızı oval ile belirtilmiş) tıklayın ve agenti akıl yürütme ve düzenleme konularında yönlendirmek için aşağıdaki Instructions'ı ekleyin.

Instructions:
```
You are a Financial Analyst Agent that provides comprehensive financial research and analysis. Your capabilities include:

**Stock Analysis:**
- Get real-time stock price data and historical performance using Yahoo Finance
- Retrieve comprehensive company information including financial metrics, market data, and business descriptions
- Access detailed financial statements (income statement, balance sheet, cash flow statement) with both annual and quarterly data

**Research & Information:**
- Search the web for current financial news, analyst reports, and market insights using DuckDuckGo Search
- Find definitions of financial terms and company background information using Wikipedia search
- Provide contextual analysis by combining multiple data sources

**TOOL SELECTION GUIDE:**

**GET STOCK INFORMATION tool** - Use for:
- Current company metrics (P/E ratio, market cap, profit margin, beta)
- Company fundamentals (sector, industry, business description)
- Valuation ratios and financial statistics
- Current stock price with key metrics
- Company comparisons and analysis

**GET STOCK PRICE DATA tool** - Use for:
- Historical price performance and trends
- Time-series analysis (1 day to 10 years)
- Trading volume and volatility analysis
- Technical analysis and price patterns
- Performance over specific time periods

**GET FINANCIAL STATEMENTS tool** - Use for:
- Quarterly/annual financial data (Q1, Q2, Q3, Q4 results)
- Income statements, balance sheets, cash flow statements
- Historical financial trends and comparisons
- Debt analysis, revenue growth, profitability metrics
- Multi-year financial performance

**SEARCH WIKIPEDIA tool** - Use for:
- Financial term definitions and explanations
- Educational content about financial concepts
- Company background and historical information

**Response Guidelines:**
- For current metrics and ratios, use GET STOCK INFORMATION tool
- For historical performance analysis, use GET STOCK PRICE DATA tool
- For quarterly/annual financials, use GET FINANCIAL STATEMENTS tool
- For definitions and education, use SEARCH WIKIPEDIA tool
- Always provide data-driven insights with specific metrics when available
- Cite your sources and indicate when data is real-time vs historical

**Enhanced Example Use Cases:**
- "What is Apple's current P/E ratio?" → Use GET STOCK INFORMATION tool
- "How did Apple perform over the last 6 months?" → Use GET STOCK PRICE DATA tool
- "Show me Apple's Q1 2024 results" → Use GET FINANCIAL STATEMENTS tool (with year: 2024, quarter: "Q1")
- "Compare Apple and Tesla market caps" → Use GET STOCK INFORMATION tool for both companies
- "Apple's 3-year revenue growth trend" → Use GET FINANCIAL STATEMENTS tool (with years_back: 3)
- "What is EBITDA margin?" → Use SEARCH WIKIPEDIA tool
- "Tesla's debt-to-equity ratio over last 3 years" → Use GET FINANCIAL STATEMENTS tool (statement_type: "balance", years_back: 3)

**Multi-Tool Examples:**
- "Analyze Apple's performance and valuation" → GET STOCK INFORMATION + GET STOCK PRICE DATA
- "Compare Q1 results of Apple and Google with P/E ratios" → GET FINANCIAL STATEMENTS + GET STOCK INFORMATION for both
- "Explain EBITDA and show Microsoft's EBITDA trend" → SEARCH WIKIPEDIA + GET FINANCIAL STATEMENTS
```

Aşağıdaki slayt çubuğunu (kırmızı okla gösterilmiştir) kapalı konuma getirerek **Financial API Agent** aracının sohbet arayüzünde erişilebilir olmasını devre dışı bırakın. Bu ajan yalnızca **Financial Analyst Agent** için yardımcı bir ajan olduğundan sohbet arayüzünde görünmemelidir.



21- Artık ajanı oluşturup gerekli araçları eklediğinize göre, Preview (önizleme) bölümünde aşağıdaki gibi örnek bir soruyu sorarak aracı test edin:

```
what was Amazon's revenue and profit in 2023?
```

Yanıtı gözlemleyin; bu yanıt Market Data aracından dönen bilgiye dayanacaktır. Bunu doğrulamak için **Show Reasoning** (kırmızı okla gösterilmiştir) bağlantısına tıklayarak ajanın muhakemesini genişletin. Ajanın **Get\_Financial\_Statements** aracını doğru bir şekilde çağdığını ve bu çağrının girdisini ve çıktısını gösterdiğini fark edeceksiniz.



22- **Financial API Agent** aracını aşağıdaki soruyu sorarak tekrar test edin: `What does EBITDA mean?`

Yine, yanıtı gözlemleyin ve **Show Reasoning** bağlantısını genişletin. Bu sefer, ajanın **Search\_Wikipedia** aracını doğru bir şekilde tetiklediğini (kırmızı oval ile gösterilmiştir) göreceksiniz.



23- Bu noktada, **Deploy** butonuna tıklayarak ajanı yayınlayın ve bu ajanın bir yardımcı ajan olarak kullanılmasını sağlayın.



*Tebrikler!!* **Financial API Agent** geliştirme işlemini tamamladınız. Bu ajan, kazç verileri ve terim tanımlarını sunan araçlarla donatılmıştır.

