---
title: Unire tabelle in modo manuale (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0299be9a1cb480a567e0b166c990d25588598aba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62711058"
---
# <a name="join-tables-manually-visual-database-tools"></a>Unione di tabelle in modo manuale (Visual Database Tools)
  Quando si aggiungono due o più tabelle a una query, in [Progettazione query e Progettazione viste](visual-database-tools.md) viene effettuato un tentativo per unirle in join sulla base dei dati comuni o delle informazioni archiviate nel database relative alla correlazione delle tabelle. Per informazioni dettagliate, vedere [Unione di tabelle in modo automatico &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md). Se tuttavia le tabelle non vengono unite in join automaticamente o se si desidera creare ulteriori condizioni di join tra le tabelle, sarà possibile il join manuale.  
  
 I join possono essere creati sulla base del confronto tra qualsiasi coppia di colonne, non solo delle colonne che contengono le stesse informazioni. Ad esempio, se il database contiene le tabelle `titles` e `roysched`, sarà possibile confrontare i valori nella colonna `ytd_sales` della tabella `titles` con le colonne `lorange` e `hirange` della tabella `roysched` . Creando questo join sarà possibile trovare i titoli le cui vendite annuali sono comprese nell'intervallo tra valori bassi e alti per il pagamento dei diritti d'autore.  
  
> [!TIP]  
>  Le operazioni di join saranno più rapide se le colonne della condizione di join vengono indicizzate. In alcuni casi, la creazione di join su colonne non indicizzate può provocare un rallentamento della query.  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>Per unire in join manualmente tabelle o oggetti con struttura di tabella  
  
1.  Aggiungere gli oggetti da unire in join al [riquadro diagramma](diagram-pane-visual-database-tools.md) .  
  
2.  Trascinare il nome della colonna join nella prima tabella o nel primo oggetto con struttura di tabella e rilasciarlo nella colonna correlata nella seconda tabella o oggetto con struttura di tabella. Non è possibile basare un join sulle colonne `text`, `ntext`, o i`mage`.  
  
    > [!NOTE]  
    >  Le colonne join devono avere tipi di dati uguali o compatibili. Se ad esempio la colonna join della prima tabella è una data, dovrà essere correlata a una colonna data nella seconda tabella. D'altra parte, se la prima colonna join contiene un valore intero, anche la colonna join correlata dovrà contenere dati di un tipo intero, anche se di dimensioni diverse. In Progettazione query e Progettazione viste non verranno verificati i tipi di dati delle colonne utilizzati per creare un join, ma quando si eseguirà la query verrà visualizzato un errore qualora i tipi di dati non siano compatibili.  
  
3.  Se necessario, cambiare l'operatore di join. L'operatore di join predefinito è il segno di uguale (=). Per informazioni dettagliate, vedere [Modifica di operatori di join &#40;Visual Database Tools&#41;](modify-join-operators-visual-database-tools.md).  
  
 In Progettazione query e Progettazione viste verrà aggiunta una clausola INNER JOIN all'istruzione SQL nel [riquadro SQL](sql-pane-visual-database-tools.md). È possibile trasformare il tipo in outer join. Per informazioni dettagliate, vedere [Creazione di join esterni &#40;Visual Database Tools&#41;](create-outer-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query con join &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
