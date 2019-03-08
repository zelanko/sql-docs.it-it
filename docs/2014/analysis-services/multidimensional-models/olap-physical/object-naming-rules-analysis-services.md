---
title: Oggetto le regole di denominazione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc4392b2c78fc2d2709a37a27b17d930af0681dd
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578414"
---
# <a name="object-naming-rules-analysis-services"></a>Regole di denominazione degli oggetti (Analysis Services)
  In questo argomento vengono descritte le convenzioni di denominazione dell'oggetto, le parole riservate e i caratteri che non possono essere utilizzati nel nome dell'oggetto, nel codice o nello script in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a> Convenzioni di denominazione  
 Ogni oggetto dispone delle proprietà `Name` e `ID` che devono essere univoche nell'ambito della raccolta padre. Ad esempio, due dimensioni possono avere lo stesso nome fintanto che ciascuna risiede in un database diverso.  
  
 Sebbene sia possibile specificarlo manualmente, l'`ID` viene solitamente generato automaticamente quando viene creato l'oggetto. È consigliabile non modificare l'`ID` una volta avviata la compilazione di un modello. In un modello tutti i riferimenti agli oggetti sono basati sull'`ID`. Pertanto, la modifica dell'`ID` può facilmente causare il danneggiamento del modello.  
  
 Gli oggetti `DataSource` e `DataSourceView` presentano eccezioni rilevanti alle convenzioni di denominazione. L'ID `DataSource` può essere impostato su un punto singolo (.), che non è univoco, come riferimento al database corrente. Una seconda eccezione è costituita da `DataSourceView`, il quale è conforme alle convenzioni di denominazione definite per gli oggetti `DataSet` in .NET Framework, dove `Name` è utilizzato come identificatore.  
  
 Di seguito vengono riportate le regole valide per le proprietà `Name` e `ID`.  
  
-   Per i nomi non viene fatta distinzione tra maiuscole e minuscole. Non è possibile avere un cubo denominato "sales" e un altro denominato "Sales" nello stesso database.  
  
-   Gli spazi iniziali o finali non sono consentiti nel nome dell'oggetto, sebbene sia possibile incorporare gli spazi all'interno del nome. Gli spazi iniziali e finali vengono eliminati in modo implicito. Ciò si applica sia alle proprietà `Name` e `ID` di un oggetto.  
  
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
|`Server`|Seguire le convenzioni di denominazione del server Windows quando si denomina un oggetto server. Visualizzare [convenzioni di denominazione (Windows)](/windows/desktop/DNS/naming-conventions) per informazioni dettagliate.|  
|`DataSource`|`: / \ * | ? " () [] {} <>`|  
|`Level` o `Attribute`|```. , ; ' ` : / \ * &| ? " & % $ ! + = [] {} \< >```|  
|`Dimension` o `Hierarchy`|```. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \<,>```|  
|Tutti gli altri oggetti|```. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \< >```|  
  
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
 [Parole riservate MDX](/sql/mdx/mdx-reserved-words)   
 [Le traduzioni &#40;Analysis Services&#41;](../../../analysis-services/translations-analysis-services.md)   
 [XML for Analysis conformità &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
