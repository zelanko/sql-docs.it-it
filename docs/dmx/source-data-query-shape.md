---
title: FORMA (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938111"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;query sull'origine dati&gt; -forma
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di combinare query da più origini dei dati in una singola tabella gerarchica, ovvero una tabella con tabelle nidificate, che diventa la tabella dei case per il modello di data mining.  
  
 La sintassi completa del **SHAPE** comando è documentato nel [!INCLUDE[msCoName](../includes/msconame-md.md)] Data Access Components (MDAC) Software Development Kit (SDK).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>Argomenti  
 *query master*  
 Query che restituisce la tabella padre.  
  
 *query di tabella figlio*  
 Query che restituisce la tabella nidificata.  
  
 *colonna master*  
 Colonna della tabella padre utilizzata per identificare le righe figlio tra i risultati di una query che restituisce una tabella figlio.  
  
 *colonna figlio*  
 Colonna della tabella figlio utilizzata per identificare le righe padre tra i risultati di una query che restituisce la tabella padre.  
  
 *nome della colonna nella tabella*  
 Nome della colonna appena aggiunta nella tabella padre per creare la tabella figlio.  
  
## <a name="remarks"></a>Note  
 Le query devono essere ordinate in base alla colonna che definisce la correlazione tra la tabella padre e la tabella figlio.  
  
## <a name="examples"></a>Esempi  
 È possibile usare l'esempio seguente all'interno di un' [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) istruzione per addestrare un modello contenente una tabella nidificata. Le due tabelle all'interno di **forma** istruzione sono correlati tramite il **OrderNumber** colonna.  
  
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
 [&#60;query sull'origine dati&#62;](../dmx/source-data-query.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
