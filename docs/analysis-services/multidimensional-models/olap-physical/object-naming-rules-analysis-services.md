---
title: Oggetto le regole di denominazione (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7267097b1a06cb44c801ed20cbfd206c330328ff
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509470"
---
# <a name="object-naming-rules-analysis-services"></a>Regole di denominazione degli oggetti (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  In questo argomento vengono descritte le convenzioni di denominazione dell'oggetto, le parole riservate e i caratteri che non possono essere utilizzati nel nome dell'oggetto, nel codice o nello script in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a> Convenzioni di denominazione  
 Ogni oggetto dispone di un **Name** e **ID** proprietà che devono essere univoci all'interno dell'ambito della raccolta padre. Ad esempio, due dimensioni possono avere lo stesso nome fintanto che ciascuna risiede in un database diverso.  
  
 Sebbene sia possibile specificare manualmente, il **ID** viene solitamente generato automaticamente quando viene creato l'oggetto. È consigliabile non modificare il **ID** una volta avviata la compilazione di un modello. Tutti i riferimenti agli oggetti in un modello di base di **ID**. Pertanto, la modifica un' **ID** può facilmente causare il danneggiamento del modello.  
  
 **DataSource** e **DataSourceView** gli oggetti sono eccezioni rilevanti delle convenzioni di denominazione. **DataSource** ID può essere impostato su un punto singolo (.), che non è univoco, come un riferimento al database corrente. Una seconda eccezione è **DataSourceView**, che è conforme alle convenzioni di denominazione definite per **set di dati** oggetti in .NET Framework, in cui il **nome** viene utilizzato come il identificatore.  
  
 Le regole seguenti riguardano **Name** e **ID** proprietà.  
  
-   Per i nomi non viene fatta distinzione tra maiuscole e minuscole. Non è possibile avere un cubo denominato "sales" e un altro denominato "Sales" nello stesso database.  
  
-   Gli spazi iniziali o finali non sono consentiti nel nome dell'oggetto, sebbene sia possibile incorporare gli spazi all'interno del nome. Gli spazi iniziali e finali vengono eliminati in modo implicito. Questo vale per entrambi i **Name** e **ID** di un oggetto.  
  
-   Il numero massimo di caratteri consentito è 100.  
  
-   Non esiste alcun particolare requisito per il primo carattere di un identificatore, che può pertanto essere qualsiasi carattere valido.  
  
##  <a name="bkmk_reserved"></a> Caratteri e parole riservate  
 Le parole riservate sono in inglese e si applicano ai nomi di oggetto, non alle didascalie. Se inavvertitamente si utilizza una parola riservata nel nome di un oggetto, viene restituito un errore di convalida. Per i modelli di data mining e multidimensionali, le parole riservate descritte di seguito non possono mai essere utilizzate in un nome di oggetto.  
  
 Per i modelli tabulari, per cui la compatibilità del database è impostata su 1103, le regole di convalida sono meno restrittive per alcuni oggetti, senza la conformità ai requisiti di caratteri estesi e alle convenzioni di denominazione di alcune applicazioni client. I database che soddisfano questi criteri sono soggetti a regole di convalida meno restrittive. In questo caso, è possibile includere in un nome di oggetto un carattere limitato e passare la convalida.  
  
 **Parole riservate**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 tramite COM9 (COM1, COM2, COM3 e così via)  
  
-   CON  
  
-   LPT1 tramite LPT9 (LPT1, LPT2, LPT3 e così via)  
  
-   NUL  
  
-   PRN  
  
-   Non è consentito utilizzare NULL come carattere in una stringa all'interno del frammento XML  
  
 **Caratteri riservati**  
  
 Nella tabella seguente sono elencati i caratteri non validi per oggetti specifici.  
  
|Object|Caratteri non validi|  
|------------|------------------------|  
|**Server**|Seguire le convenzioni di denominazione del server Windows quando si denomina un oggetto server. Visualizzare [convenzioni di denominazione (Windows)](/windows/desktop/DNS/naming-conventions) per informazioni dettagliate.|  
|**DataSource**|: / \ * &#124; ? "[] () {} <>|  
|**Livello** o **attributo**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} < >|  
|**Dimensione** o **gerarchia**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] () {} \<, >|  
|Tutti gli altri oggetti|. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] () {} < >|  
  
 **Eccezioni: Quando sono consentiti i caratteri riservati**  
  
 Come indicato, i database di un livello specifico di compatibilità e modalità possono avere nomi di oggetto contenenti caratteri riservati. I nomi di oggetto KPI, misura, livello, gerarchia e attributo di dimensione possono contenere caratteri riservati per i database tabulari (1103 o superiore) che consentono l'utilizzo dei caratteri estesi:  
  
|Livello di compatibilità del database e modalità del server|Caratteri riservati consentiti?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (tutte le versioni)|No|  
|Tabulare - 1050|No|  
|Tabulare - 1100|No|  
|Tabulare - 1130 e superiore|Yes|  
  
 I database possono avere un oggetto ModelType predefinito. L'impostazione predefinita è equivalente a multidimensionale e pertanto non supporta l'utilizzo dei caratteri riservati nei nomi delle colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Parole riservate MDX](../../../mdx/mdx-reserved-words.md)   
 [Supporto delle traduzioni in Analysis Services](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis conformità &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
