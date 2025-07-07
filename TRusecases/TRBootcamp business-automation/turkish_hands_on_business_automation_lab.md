# 👨🏻‍💻 Kullanım Senaryosu: İş Otomasyonu   

## İçindekiler
- [Mimari](#-mimari)
- [Kullanım Senaryosu Açıklaması](#kullanım-senaryosu-açıklaması)
- [Ön Koşullar](#ön-koşullar)
- [Agent Lab - watsonx.ai](#agent-lab---watsonxai)
  - [Comparison Agent](#comparison-agent)
    - [Kurulum](#kurulum)
    - [Yapılandırma](#yapılandırma)
    - [Araçlar](#araçlar)
    - [Kaydetme ve Dağıtım](#kaydetme-ve-dağıtım)
- [watsonx.ai'nin agent'ını watsonx Orchestrate'de Harici Agent olarak Entegre Etme](#watsonxainin-agentını-watsonx-orchestratede-harici-agent-olarak-entegre-etme)
- [Orchestrate Agent](#orchestrate-agent)
  - [Product Agent](#product-agent)
- [Agent'ları Çalışırken Deneyimleyin](#agentları-çalışırken-deneyimleyin)


## 🏛 Mimari  

<img width="900" alt="image" src="assets/Business_Automation_Architecture.png">

## Kullanım Senaryosu Açıklaması

Otomotiv sektörünün büyük oyuncusu ABC Motor Corp'un satış departmanı, satış teklifleri hazırlarken rakip ürünlerin özelliklerini anlamak ve bunları kendi ürünleriyle karşılaştırmak için çok fazla zaman harcıyordu. ABC Motor Corp, satış ekiplerinin ürünlerini rakiplerine karşı hızlı bir şekilde tanımlamasına ve konumlandırmasına yardımcı olacak otomatik bir rekabet analizi sistemine ihtiyaç duyuyor. Geleneksel olarak, rakip bilgilerini toplama kapsamlı manuel araştırma gerektiriyordu, bu da verimsiz ve güncel olmayan bilgilere açık hale getiriyordu. Bu nedenle, bu kullanım senaryosunun amacı, müşterinin rekabet analizi ve pazar araştırmasını destekleyen AI destekli bir sistem oluşturmaktır.

## Ön Koşullar

- Devam etmeden önce **tüm sistemlerin** çalışır durumda olduğundan emin olmak için eğitmeninizle kontrol edin.
- API anahtarı oluşturma, proje kurulumu ve ilgili yapılandırmalar için lütfen [environment-setup](/environment-setup) kılavuzunu inceleyin.
- Bu laboratuvarı yöneten bir eğitmenseniz, tüm ortamları ve sistemleri kurmak için **Eğitmen kılavuzlarını** kontrol edin.

## Agent Lab - watsonx.ai

>**Not:** Agent oluşturmaya başlamadan önce, watsonx.ai instance'ınızın API anahtarını oluşturduğunuzdan emin olun. 

Bu kurulumun parçası olarak watsonx.ai'nin Agent Lab'ında bir agent **Comparison Agent** oluşturacağız:  

Agent Lab'ın Ana sayfasından, görevleri otomatikleştirmek için bir AI agent oluştur'a tıklayın

![Home page](assets/agent_lab_home.png) 

**Comparison Agent** ile başlayalım. 

### Comparison Agent  
#### Kurulum  
1. Resimde gösterildiği gibi agent için bir **isim** girin.
2. Bir **açıklama** ekleyin (isteğe bağlı).
```
The agent compares the given data with additional information gathered from Google search results.
```
![Setup](assets/config_CA.png)  

#### Yapılandırma    
1. Framework olarak **LangGraph**'ı seçin.  
2. Mimari olarak **ReAct**'ı seçin. 
3. Resimde gösterildiği gibi **Talimatları** girin. Bu talimatlar, agent'ınızın hangi görevleri yerine getirmesi gerektiği konusunda rehberlik eder. Bunun için aşağıdaki prompt'u kullanabilirsiniz.
```
You are an expert of automobile industry combining given details present in your context window.  Your task is crawl and search the Top 3 product URLs (strictly from the automobile industry) and to analyse and compare products on the following features strictly: Range, Pricing, Acceleration, Top Speed, Interior and Safety Features If a feature is not applicable, mark it as N/A. Additionally, perform a SWOT analysis of top products (Strengths, Weaknesses, Opportunities, and Threats) Present the comparison in 3 tables one for the comparison , second for the rating numerical rating (X/5) and a star rating (★ out of ★★★★★) for each feature  and  third for the SWOT analysis. Give heading to each table . After every table give two divider.
Instructions:
1. When asked for competitors of the given product, make sure that you provide only the name of the products and URLs of the products below the corresponding name.
2. The generated product URLs must be strictly from the automobile industry.
3. Title for Table 1: Feature Comparison
4. Title for Table 2: Rating Comparison
5. Make sure that the Rating Comparison table has both the numerical(X/5) and star rating(★ out of ★★★★★)
6. The products should be the column names in all the tables.
7. The font of the Table Title must be bold and the font size must be 40% bigger as compared to the rest of the text.
8. Add appropriate space between each section in the table.
9. Name the References as Competitors
```
![Configuration](assets/config_CA_2.png)  


> **Not:** Google Search Tool varsayılan olarak Agent'a eklenir. Ancak, yanlışlıkla silme simgesine tıklarsanız, aşağıdaki Araç adımlarını izleyin. Aksi takdirde, bu adımı atlayabilirsiniz.

#### Araçlar  

1. Add Tool'a tıklayın.
![Add Tool](assets/add_tool.png)

2. Veri toplamak için araç olarak **Google Search**'ü seçin.  
![Tool](assets/tool_link_search_agent.png)  

#### Kaydetme ve Dağıtım
Agent oluşturulduktan sonra.

1. Agent'ınızı kaydetmek için **Save As** düğmesine tıklayın
2. agent'ı dağıtmak için **Deploy** düğmesine tıklayın.
![Comparison Agent 1](assets/config_CA_3.png) 
3. Save as düğmesine tıkladıktan sonra Agent'ı seçin (1 olarak işaretlenmiş) ve Save'e tıklayın (2 olarak işaretlenmiş)
![Comparison Agent 2](assets/config_CA_4.png)
4. Deploy'a tıkladığınızda, bir kullanıcı api anahtarı oluşturmanız gerekir. "Create"'e tıklayın.
![Comparison Agent 3](assets/image44.0.1.png)
5. Başka bir web sayfasına yönlendirileceksiniz. "Create a key"'e tıklayın.
![Comparison Agent 4](assets/image44.0.2.png)
6. Anahtar oluşturulduktan sonra, dağıtım sayfasına geri dönün. "Reload"'a tıklayın.
![Comparison Agent 4](assets/image44.1.png)
7. Dağıtım düğmesine tıkladıktan sonra Hedeflenen dağıtım alanınızın seçilmiş ve tamamlanmış olduğundan emin olun, değilse lütfen seçin (1 olarak işaretlenmiş), agent'ı dağıtmak için Deploy'a tıklayın (2 olarak işaretlenmiş)
![Comparison Agent 5](assets/config_CA_5.png)

> **BAŞARDIN! İlk AI Agent'ınızı oluşturdunuz ve dağıttınız.**
> Şimdi daha fazla agent oluşturalım ve bunları birbirine entegre edelim.

## watsonx.ai'nin agent'ını watsonx Orchestrate'de Harici Agent olarak Entegre Etme

Agent'ınızı Orchestrate'de dağıtmak için aşağıdaki adımları izleyin: 

1. watsonx.ai Agent Lab'ın ana sayfasına gidin.
![Home page](assets/agent_lab_homepage.png)

2. Hamburger menüsüne tıklayın ve **Deployments**'ı seçin.  
![Deployments](assets/hamberger_agent_lab.png)

3. **Spaces** sekmesine tıklayın ve agent'ı dağıttığınız alanı seçin.  
![Spaces](assets/ca_dep.png)

4. **Assets** sekmesine tıklayın ve agent'ı seçin.  
![Asset tab](assets/ca_dep2.png)

5. Daha sonra ana dağıtım sayfasına gideceksiniz, listeden agent'ınızı seçin.
![Deployment agent](assets/ca_dep3.png)

6. Daha sonra public endpoint stream'i kopyalayın.
![Deployment agent](assets/ca_url.png)

Şimdi Orchestrate'e gidelim ve başka bir agent oluşturup bu agent'ı ona import edelim.

## Orchestrate Agent

Orchestrate'de, aşağıda özetlenen ana agent'ımızı oluşturacağız:

### Product Agent

1. Orchestrate ana sayfasına gidin, hamburger menüsüne (☰) tıklayın, Build'i seçin ve ardından Agent Builder'ı seçin.
![Agent Builder](assets/agent_build_wxo.png)

2. Create Agent düğmesine tıklayın.
![Create Agent](assets/create_wxo.png)

3. Create from scratch'i seçin (aşağıdaki resim 1'de gösterildiği gibi), agent'ınızın adını girin (resim 2'de gösterildiği gibi), bir açıklama sağlayın (resim 3'te gösterildiği gibi) ve ardından Create düğmesine tıklayın (resim 4'te gösterildiği gibi).

   Product Agent için aşağıdaki açıklamayı kullanın
        
   ```
   This agent is designed to search for a specified product and retrieve its details and features using Retrieval-Augmented Generation (RAG) on the product catalog. It presents the information in a clear and structured format, ensuring systematic organization of key product data, making it easy to understand and use.
   ```
   ![Create from scratch](assets/product_scratch.png)

4. Agent oluşturulduktan sonra, Agent Configuration sayfasına gidin.

   **Açıklama:**
   ```
   Your knowledge base is the document that contains all the product-related information. All queries related to the product will be addressed using this document as the primary source.
   ```
   ![Knowledge](assets/product_knowledge.png)

5. Knowledge bölümüne kaydırın, ardından Document bölümünde Upload file düğmesine tıklayın ve [ürün kataloğunu](./assets/ABC_Motor_Product_Catalog.pdf) yükleyin.
![Upload file](assets/upload_file.png)

6. Toolset bölümüne kaydırın, ardından Agents bölümünde Add Agent düğmesine tıklayın.
![Add Agent](assets/add_agent_pa.png)

7. Açılır menüden Import'u seçin.
![Add from local instance](assets/import_ca.png)

> **Not:** : Şimdi Comparison Agent'ı (harici bir agent) Product Agent'a ekliyoruz, bu da ona görevleri onlara devretmesini sağlıyor.

8. Bir sonraki sayfada, External Agent'ın seçili olduğundan emin olun (aşağıdaki resim 1'de gösterildiği gibi). Zaten seçili değilse, lütfen seçin, ardından Next düğmesine tıklayın (resim 2'de gösterildiği gibi).
![Select External Agent](assets/external_agent_select.png)

9. Bir sonraki sayfada, aşağıdaki bilgileri girin:
      1. Provide: Açılır menüden watsonx.ai'yi seçin.
      2. API key: watsonx.ai API anahtarını girin.
      3. Service instance URL: 6. adımda kopyaladığımız agent'ın public endpoint URL'sini girin.
      4. Display name: Agent'ın adını girin.
      5. Description: Aşağıdaki açıklamayı girin.
      6. Import Agent düğmesine tıklayın.

**Açıklama:**
   ```
   This agent is designed to search for competitive URLs of input product and compare the given compare the given data with additional information gathered from Google search results. Its task is to carefully analyze the input data, extract key insights, and identify both differences and similarities. The findings should be presented in a well-structured table format, making it easy to understand and compare the information at a glance.

   ```
   ![External Agent](assets/external_agent_setup.png)

10. Devredilen agent'lar eklendikten sonra, aşağıdaki resimde gösterildiği gibi görüneceklerdir.
![Delegation Agent](assets/agent_appear_delegation.png)

11. Behavior bölümüne kaydırın, resimde 1 olarak gösterilen açıklamayı ekleyin ve ardından resimde 2 olarak gösterilen Deploy düğmesine tıklayın.

      Product Agent için Behavior bölümünde aşağıdaki açıklamayı kullanın.

      ```
      This agent is responsible for handling product-related queries using Retrieval-Augmented Generation (RAG) on the product catalog.
      For general product queries, it retrieves structured information directly from the knowledge base.
      For queries involving URLs or web references or comparison, it delegates the task to the Comparison Agent.
      ```
      ![Behavior](assets/Product_agent_deploy.png)

> **Not:** : Product Agent artık ürünle ilgili sorguları ele almaya hazır, görevleri Link Search Agent ve Comparison Agent'a gerektiğinde devrediyor.

## Agent'ları Çalışırken Deneyimleyin
Yukarıdaki adımları takip edin, ardından bu örnek sorgularla kullanım senaryosu ile etkileşim kurmayı deneyin:

1. Product Agent

   Product Agent'tan yanıt almak için aşağıdaki soruları sorun:
   ```
   S1: ABC Motors'un ürünleri nelerdir?
   ```
   ```
   S2: Zenith X3 hakkında bilgi ver.
   ```
   ![Product Agent Response](assets/chat_1.png)  

3. Comparison Agent

   Alınan verileri karşılaştırmak için şunu sorun:
   ```
   Yukarıdaki ürünün rakiplerinin URL'lerini ver ve karşılaştırmayı da göster.
   ```
   ![Comparison Agent Response](assets/chat_2.png)  
   ![Comparison Agent Response 2](assets/chat_3.png)

Şimdi keşfedin ve Skills & Agents'ın gücünü çalışırken deneyimleyin! 🚀