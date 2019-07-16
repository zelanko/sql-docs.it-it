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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165462"
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
 Le parole riservate sono in inglese e si applicano ai nomi di oggetto, non alle didascalie. Se si utilizza inavvertitamente una parola riservata in un nome di oggetto, si verificherà un errore di convalida. Per i modelli di data mining e multidimensionali, le parole riservate descritte di seguito non possono mai essere utilizzate in alcun nome di oggetto.  
  
 Per i modelli tabulari dove la compatibilità di database è impostata su 1103, le regole di convalida sono state rese flessibili per alcuni oggetti, non conformi per i requisiti di caratteri estesi e le convenzioni di denominazione di alcune applicazioni client. I database che soddisfano questi criteri sono soggetti a regole di convalida meno restrittive. In questo caso è possibile che un nome di oggetto includa un carattere limitato e superi comunque la convalida.  
  
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
|**Livello** o **attributo**|. , ; ' ` : / \ * &#124; ? "& % $! + = [] {} < >|  
|**Dimensione** o **gerarchia**|. , ; ' ` : / \ * &#124; ? "& % $! + = [] () {} \<, >|  
|Tutti gli altri oggetti|. , ; ' ` : / \ * &#124; ? "& % $! + = [] () {} < >|  
  
 **Eccezioni: Quando sono consentiti i caratteri riservati**  
  
 Come è stato notato, i database di un livello di compatibilità e di modalità specifico possono avere nomi di oggetti che includono caratteri riservati. I nomi di attributi della dimensione, gerarchie, livelli, misuri e oggetti KPI possono includere caratteri riservati, per database tabulari (1103 o un valore superiore) che consentono l'utilizzo di caratteri estesi:  
  
|Livello di compatibilità del database e modalità del server|Caratteri riservati consentiti?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (tutte le versioni)|No|  
|Tabulare - 1050|No|  
|Tabulare - 1100|No|  
|Tabulare - 1130 e superiore|Yes|  
  
 I database possono avere un valore ModelType predefinito. Il valore predefinito è equivalente a multidimensionale e quindi non supporta l'utilizzo di caratteri riservati nei nomi delle colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Parole riservate MDX](../../../mdx/mdx-reserved-words.md)   
 [Supporto delle traduzioni in Analysis Services](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis conformità &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
