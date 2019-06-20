---
title: Opzione di configurazione del server transform noise words | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5ddad15af74e45313d3e71b059fae36d166560
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808692"
---
# <a name="transform-noise-words-server-configuration-option"></a>Opzione di configurazione del server transform noise words Server
  Usare la `transform noise words` opzione di configurazione server per eliminare un messaggio di errore se parole non significative, vale a dire [parole non significative](../../relational-databases/search/full-text-search.md), esecuzione di un'operazione booleana su una query full-text restituisce zero righe. Questa opzione è utile per le query full-text in cui viene utilizzato il predicato CONTAINS e con operazioni booleane o operazioni NEAR che includono parole non significative. I valori possibili sono illustrati nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Le parole non significative non vengono trasformate. Quando una query full-text contiene parole non significative, la query restituisce zero righe e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene generato un avviso. Questo è il comportamento predefinito.<br /><br /> Si noti che l'avviso è un avviso di run-time. Pertanto, se la clausola full-text nella query non viene eseguita, l'avviso non viene generato. Per una query locale, viene generato un solo avviso, anche se sono presenti più clausole di query full-text. Per una query remota, il server collegato potrebbe non inoltrare l'errore ed è pertanto possibile che l'avviso non venga generato.|  
|1|Le parole non significative vengono trasformate. Tali parole vengono ignorate e viene valutato e il resto della query.<br /><br /> Se vengono specificate parole non significative in un termine di prossimità, queste vengono rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La parola non significativa `is` viene ad esempio rimossa da `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`, trasformando la query di ricerca in `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`. Si noti che la query `CONTAINS(<column_name>, 'NEAR(hello,is)')` verrebbe trasformata semplicemente in `CONTAINS(<column_name>, hello)` in quanto vi è un solo termine di ricerca valido.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Effetti dell'impostazione transform noise words  
 In questa sezione viene illustrato il comportamento di query che contengono una parola non significativa, "`the`", quando vengono utilizzate le impostazioni alternative di `transform noise words`.  Si presuppone che le stringhe di query full-text di esempio vengano eseguite su una riga di tabella che contiene i dati seguenti: `[1, "The black cat"]`.  
  
> [!NOTE]  
>  In tutti gli scenari di questo tipo può venire generato un avviso di parola non significativa.  
  
-   Con transform noise words impostato su 0:  
  
    |Stringa query|Risultato|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Nessun risultato (il comportamento è lo stesso per "`the`" AND "`cat`").|  
    |"`cat`" NEAR "`the`"|Nessun risultato (il comportamento è lo stesso per "`the`" NEAR "`cat`").|  
    |"`the`" AND NOT "`black`"|Nessun risultato|  
    |"`black`" AND NOT "`the`"|Nessun risultato|  
  
-   Con transform noise words impostato su 1:  
  
    |Stringa query|Risultato|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Riscontro per la riga con ID 1|  
    |"`cat`" NEAR "`the`"|Riscontro per la riga con ID 1|  
    |"`the`" AND NOT "`black`"|Nessun risultato|  
    |"`black`" AND NOT "`the`"|Riscontro per la riga con ID 1|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente il valore di `transform noise words` viene impostato su `1`.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
