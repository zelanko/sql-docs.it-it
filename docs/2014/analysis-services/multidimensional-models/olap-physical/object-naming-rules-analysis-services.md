---
title: Regole di denominazione degli oggetti (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6adfd4b23b6fe9129641271fc3c2381e161119ea
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545889"
---
# <a name="object-naming-rules-analysis-services"></a>Regole di denominazione degli oggetti (Analysis Services)
  In questo argomento vengono descritte le convenzioni di denominazione dell'oggetto, le parole riservate e i caratteri che non possono essere utilizzati nel nome dell'oggetto, nel codice o nello script in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="naming-conventions"></a><a name="bkmk_Names"></a>Convenzioni di denominazione  
 Ogni oggetto dispone di una proprietà `Name` e `ID` che deve essere univoca nell'ambito della raccolta padre. Ad esempio, due dimensioni possono avere lo stesso nome fintanto che ciascuna risiede in un database diverso.  
  
 Sebbene sia possibile specificarlo manualmente, l'`ID` viene solitamente generato automaticamente quando viene creato l'oggetto. Si consiglia di non modificare mai la proprietà `ID` una volta avviata la compilazione di un modello. In un modello tutti i riferimenti agli oggetti sono basati sull'`ID`. Pertanto, la modifica dell'`ID` può facilmente causare il danneggiamento del modello.  
  
 Gli oggetti `DataSource` e `DataSourceView` presentano eccezioni rilevanti alle convenzioni di denominazione. L'ID `DataSource` può essere impostato su un punto singolo (.), che non è univoco, come riferimento al database corrente. Una seconda eccezione è `DataSourceView`, che aderisce alle convenzioni di denominazione definite per gli oggetti `DataSet` in .NET Framework, dove la proprietà `Name` viene utilizzata come identificatore.  
  
 Le regole seguenti si applicano alle proprietà `Name` e `ID`.  
  
-   Per i nomi non viene fatta distinzione tra maiuscole e minuscole. Non è possibile avere un cubo denominato "Sales" e un altro denominato "Sales" nello stesso database.  
  
-   Gli spazi iniziali o finali non sono consentiti nel nome dell'oggetto, sebbene sia possibile incorporare gli spazi all'interno del nome. Gli spazi iniziali e finali vengono eliminati in modo implicito. Ciò si applica sia alle proprietà `Name` e `ID` di un oggetto.  
  
-   Il numero massimo di caratteri consentito è 100.  
  
-   Non esiste alcun particolare requisito per il primo carattere di un identificatore, che può pertanto essere qualsiasi carattere valido.  
  
##  <a name="reserved-words-and-characters"></a><a name="bkmk_reserved"></a>Parole riservate e caratteri  
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
  
|Oggetto|Caratteri non validi|  
|------------|------------------------|  
|`Server`|Seguire le convenzioni di denominazione del server Windows quando si denomina un oggetto server. Per informazioni dettagliate, vedere [convenzioni di denominazione (Windows)](/windows/desktop/DNS/naming-conventions) .|  
|`DataSource`| `: / \ * \| ? " () [] {} <>` |  
|`Level` o `Attribute`|````. , ; ' ` : / \ * & \| ? " & % $ ! + = [] {} < >````|  
|`Dimension` o `Hierarchy`|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} <,>````|  
|Tutti gli altri oggetti|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} < >````|  
  
 **Eccezioni: quando sono consentiti i caratteri riservati**  
  
 Come è stato notato, i database di un livello di compatibilità e di modalità specifico possono avere nomi di oggetti che includono caratteri riservati. I nomi di attributi della dimensione, gerarchie, livelli, misuri e oggetti KPI possono includere caratteri riservati, per database tabulari (1103 o un valore superiore) che consentono l'utilizzo di caratteri estesi:  
  
|Livello di compatibilità del database e modalità del server|Caratteri riservati consentiti?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (tutte le versioni)|No|  
|Tabulare - 1050|No|  
|Tabulare - 1100|No|  
|Tabulare-1130 e versioni successive|Sì|  
  
 I database possono avere un valore ModelType predefinito. Il valore predefinito è equivalente a multidimensionale e quindi non supporta l'utilizzo di caratteri riservati nei nomi delle colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Parole riservate MDX](/sql/mdx/mdx-reserved-words)   
 [Traduzioni &#40;Analysis Services&#41;](/analysis-services/translation-support-in-analysis-services)   
 [XML for Analysis di conformità &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
