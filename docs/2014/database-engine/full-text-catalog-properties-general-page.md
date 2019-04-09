---
title: Proprietà catalogo full-Text (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: be73ed98700ef261ccee026469dddd22017998e0
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241450"
---
# <a name="full-text-catalog-properties-general-page"></a>Proprietà catalogo full-text (pagina Generale)
  Questa sezione illustra le opzioni e le funzioni disponibili nella **generali** pagina della **proprietà catalogo Full-Text** nella finestra di dialogo.  
  
> [!NOTE]  
>  Per i database di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], un catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text. Il catalogo full-text è un oggetto virtuale che non appartiene ad alcun filegroup.  
  
## <a name="options"></a>Opzioni  
  
### <a name="properties"></a>Proprietà  
 **Catalogo predefinito**  
 Indica se il catalogo è quello predefinito per il database.  
  
 **Stato popolamento**  
 Indica lo stato del catalogo. I valori possibili sono:  
  
-   **Idle**  
  
-   **Ricerca per indicizzazione in corso**  
  
-   **In sospeso**  
  
-   **Sospensione causata dal servizio Microsoft FullText**  
  
-   **Recupero in seguito a un'interruzione in corso**  
  
-   **Shutdown**  
  
-   **Popolamento incrementale del catalogo in corso**  
  
-   **Compilazione dell'indice in corso**  
  
-   **Il disco è in pausa full**  
  
-   **Rilevamento modifiche**  
  
 **Conteggio elementi**  
 Consente di visualizzare il numero di elementi full-text presenti nel catalogo.  
  
 **Dimensioni catalogo**  
 Consente di visualizzare le dimensioni in megabyte del catalogo full-text.  
  
 **Nome**  
 Nome del catalogo full-text.  
  
 **Distinzione caratteri accentati/non accentati**  
 Visualizzare o modificare se il catalogo è sensibile ai segni diacritici, ad esempio una tilde (**~**), mark latino (**'**), o umlaut (**¨**). I valori validi sono:  
  
-   **No**  
  
-   **Yes**  
  
-   Per informazioni sui segni diacritici, vedere [segni diacritici](https://www.merriam-webster.com/dictionary/diacritic) nel dizionario Merriam inventa.  
  
 **Data ultimo popolamento**  
 Consente di visualizzare la data dell'ultimo popolamento del catalogo.  
  
 **Proprietario**  
 Proprietario del catalogo full-text.  
  
 **Conteggio chiavi univoche**  
 Numero di parole univoche che costituiscono l'indice full-text del catalogo.  
  
### <a name="catalog-action"></a>Azione catalogo  
  
|||  
|-|-|  
|**None**|Non esegue le operazioni **Ottimizza catalogo**, **Ricompila catalogo**o **Ripopola catalogo** .|  
|**Ottimizza catalogo**|Consente di ottimizzare l'utilizzo di spazio del catalogo e di migliorare le prestazioni di query, nonché di migliorare l'accuratezza della classificazione della pertinenza dei risultati delle ricerche.<br /><br /> Verrà eseguito ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE.|  
|**Ricompila catalogo**|Consente di eliminare e ricompilare il catalogo full-text. È necessario eseguire questa operazione quando viene modificata una proprietà fondamentale del catalogo, ad esempio l'impostazione relativa alla distinzione dei caratteri accentati e non accentati.<br /><br /> Affinché l'operazione di ricompilazione abbia esito positivo, il filegroup in cui risiede il catalogo full-text deve essere online oppure di lettura e scrittura. Al termine della ricompilazione, l'indice full-text verrà ripopolato.<br /><br /> Verrà eseguito ALTER FULLTEXT CATALOG *catalog_name* RICOMPILARE.|  
|**Ripopola catalogo**|Consente di aggiornare il catalogo con le modifiche più recenti apportate ai dati. Questa opzione implica tempi di inattività del catalogo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Popolamento degli indici full-text](../relational-databases/indexes/indexes.md)  
  
  
