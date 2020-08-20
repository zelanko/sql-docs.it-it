---
description: '&lt;query dei dati &gt; di origine-forma'
title: SHAPE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16fff086514facbb8197d8d6f27b72b81f67c2e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500792"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;query dei dati &gt; di origine-forma
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Consente di combinare query da più origini dei dati in una singola tabella gerarchica, ovvero una tabella con tabelle nidificate, che diventa la tabella dei case per il modello di data mining.  
  
 La sintassi completa del comando **Shape** è documentata nel [!INCLUDE[msCoName](../includes/msconame-md.md)] Software Development Kit (SDK) di Data Access Components (MDAC).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SHAPE {<primary query>}  
APPEND ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>Argomenti  
 *query primaria*  
 Query che restituisce la tabella padre.  
  
 *query tabella figlio*  
 Query che restituisce la tabella nidificata.  
  
 *colonna primaria*  
 Colonna della tabella padre utilizzata per identificare le righe figlio tra i risultati di una query che restituisce una tabella figlio.  
  
 *colonna figlio*  
 Colonna nella tabella figlio per identificare la riga padre dal risultato di una query primaria.  
  
 *Nome tabella colonne*  
 Nome della colonna appena aggiunta nella tabella padre per creare la tabella figlio.  
  
## <a name="remarks"></a>Osservazioni  
 Le query devono essere ordinate in base alla colonna che definisce la correlazione tra la tabella padre e la tabella figlio.  
  
## <a name="examples"></a>Esempi  
 Per eseguire il training di un modello contenente una tabella nidificata, è possibile utilizzare l'esempio seguente all'interno di un'istruzione [INSERT INTO &#40;&#41;DMX ](../dmx/insert-into-dmx.md) . Le due tabelle all'interno dell'istruzione **Shape** sono correlate tramite la colonna **OrderNumber** .  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#60;query sui dati di origine&#62;](../dmx/source-data-query.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
