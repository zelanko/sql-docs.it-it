---
title: Opzione di configurazione del server transform noise words | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
manager: jroth
ms.openlocfilehash: 57c63cde99dc8319e998277ab1d4c1120c8bf73f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775272"
---
# <a name="transform-noise-words-server-configuration-option"></a>Opzione di configurazione del server transform noise words Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Usare l'opzione di configurazione del server **transform noise words** per evitare la visualizzazione di un messaggio di errore se, a causa di [parole non significative](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md), un'operazione booleana su una query full-text restituisce zero righe. Questa opzione è utile per le query full-text in cui viene utilizzato il predicato CONTAINS e con operazioni booleane o operazioni NEAR che includono parole non significative. I valori possibili sono illustrati nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|Le parole non significative non vengono trasformate. Quando una query full-text contiene parole non significative, la query restituisce zero righe e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene generato un avviso. Questo è il comportamento predefinito.<br /><br /> Nota: l'avviso è un avviso di runtime. Pertanto, se la clausola full-text nella query non viene eseguita, l'avviso non viene generato. Per una query locale, viene generato un solo avviso, anche se sono presenti più clausole di query full-text. Per una query remota, il server collegato potrebbe non inoltrare l'errore ed è pertanto possibile che l'avviso non venga generato.|  
|1|Le parole non significative vengono trasformate. Tali parole vengono ignorate e viene valutato e il resto della query.<br /><br /> Se vengono specificate parole non significative in un termine di prossimità, queste vengono rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La parola non significativa `is` viene ad esempio rimossa da `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`, trasformando la query di ricerca in `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`. Si noti che la query `CONTAINS(<column_name>, 'NEAR(hello,is)')` verrebbe trasformata semplicemente in `CONTAINS(<column_name>, hello)` in quanto vi è un solo termine di ricerca valido.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Effetti dell'impostazione transform noise words  
 Questa sezione illustra il comportamento delle query che contengono una parola non significativa, "`the`", quando vengono usate le impostazioni alternative di **transform noise words**.  Si presuppone che le stringhe di query full-text di esempio vengano eseguite su una riga di tabella che contiene i dati seguenti: `[1, "The black cat"]`.  
  
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
 L'esempio seguente imposta **transform noise words** su `1`.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
  
