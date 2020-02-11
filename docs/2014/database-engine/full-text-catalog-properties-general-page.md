---
title: Proprietà catalogo full-text (pagina generale) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779664"
---
# <a name="full-text-catalog-properties-general-page"></a>Proprietà catalogo full-text (pagina Generale)
  In questa sezione vengono illustrate le opzioni e le funzioni disponibili nella pagina **generale** della finestra di dialogo **Proprietà catalogo full-text** .  
  
> [!NOTE]  
>  Per i database di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], un catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text. Il catalogo full-text è un oggetto virtuale che non appartiene ad alcun filegroup.  
  
## <a name="options"></a>Opzioni  
  
### <a name="properties"></a>Proprietà  
 **Catalogo predefinito**  
 Indica se il catalogo è quello predefinito per il database.  
  
 **Stato popolamento**  
 Indica lo stato del catalogo. Valori possibili:  
  
-   **Idle**  
  
-   **Ricerca per indicizzazione in corso**  
  
-   **Paused**  
  
-   **Sospensione causata dal servizio Microsoft FullText**  
  
-   **Ripristino**  
  
-   **Arresto**  
  
-   **Popolamento incrementale del catalogo in corso**  
  
-   **Compilazione dell'indice in corso**  
  
-   **Il disco è completamente sospeso**  
  
-   **Change tracking**  
  
 **Item Count**  
 Consente di visualizzare il numero di elementi full-text presenti nel catalogo.  
  
 **Dimensioni catalogo**  
 Consente di visualizzare le dimensioni in megabyte del catalogo full-text.  
  
 **Nome**  
 Nome del catalogo full-text.  
  
 **Distinzione tra caratteri accentati**  
 Consente di visualizzare o modificare se il catalogo è sensibile ai segni diacritici, ad esempio una**~** tilde (), un contrassegno acuto acuto (**́**) o una diereszione (**̈**). I valori validi sono:  
  
-   **No**  
  
-   **Sì**  
  
-   Per informazioni sui segni diacritici, vedere [segni diacritici](https://www.merriam-webster.com/dictionary/diacritic) nel dizionario Merriam-Webster.  
  
 **Data ultimo popolamento**  
 Consente di visualizzare la data dell'ultimo popolamento del catalogo.  
  
 **Proprietario**  
 Proprietario del catalogo full-text.  
  
 **Conteggio chiavi univoche**  
 Numero di parole univoche che costituiscono l'indice full-text del catalogo.  
  
### <a name="catalog-action"></a>Azione catalogo  
  
|||  
|-|-|  
|**Nessuno**|Non esegue le operazioni **Ottimizza catalogo**, **Ricompila catalogo**o **Ripopola catalogo** .|  
|**Ottimizza catalogo**|Consente di ottimizzare l'utilizzo di spazio del catalogo e di migliorare le prestazioni di query, nonché di migliorare l'accuratezza della classificazione della pertinenza dei risultati delle ricerche.<br /><br /> Questa azione esegue ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE.|  
|**Ricompila catalogo**|Consente di eliminare e ricompilare il catalogo full-text. È necessario eseguire questa operazione quando viene modificata una proprietà fondamentale del catalogo, ad esempio l'impostazione relativa alla distinzione dei caratteri accentati e non accentati.<br /><br /> Affinché l'operazione di ricompilazione abbia esito positivo, il filegroup in cui risiede il catalogo full-text deve essere online oppure di lettura e scrittura. Al termine della ricompilazione, l'indice full-text verrà ripopolato.<br /><br /> Questa azione esegue ALTER FULLTEXT CATALOG *catalog_name* Rebuild.|  
|**Ripopola catalogo**|Consente di aggiornare il catalogo con le modifiche più recenti apportate ai dati. Questa opzione implica tempi di inattività del catalogo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Popolamento degli indici full-text](../relational-databases/indexes/indexes.md)  
  
  
