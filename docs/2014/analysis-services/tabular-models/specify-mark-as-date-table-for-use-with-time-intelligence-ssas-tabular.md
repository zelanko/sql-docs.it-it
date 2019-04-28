---
title: Specificare contrassegna come tabella data per l'uso con Intelligence in tempo (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af799e8e806696022635a04d808213ffb5c0e779
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794302"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a>Specificare Contrassegna come tabella data per l'utilizzo con funzionalità di Business Intelligence per le gerarchie temporali (SSAS tabulare)
  Per utilizzare le funzionalità di Business Intelligence per le gerarchie temporali nelle formule DAX, è necessario specificare una tabella relativa alla data e una colonna (datetime) dell'identificatore univoco del tipo di dati Date. Una volta specificata una colonna nella tabella relativa alla data come identificatore univoco, è possibile creare le relazioni tra le colonne nella tabella in questione e tutte le tabelle dei fatti.  
  
 In caso di utilizzo delle funzioni di Business Intelligence per le gerarchie temporali, sono valide le regole seguenti:  
  
-   Quando si utilizzano funzioni di Business Intelligence per le gerarchie temporali di DAX, non specificare mai una colonna di tipo datetime da una tabella dei fatti. Creare sempre una tabella relativa alla data separata nel modello con almeno un colonna di tipo datetime con tipo di dati Date e con valori univoci.  
  
-   Verificare che la tabella relativa alla data disponga di un intervallo di date continuo.  
  
-   È consigliabile che la granularità della colonna di tipo datetime nella tabella relativa alla data sia a livello di giorno, senza frazioni di un giorno.  
  
-   È necessario specificare una tabella relativa alla data e una colonna dell'identificatore univoco utilizzando la finestra di dialogo **Contrassegna come tabella data** .  
  
-   Creare le relazioni tra le tabelle dei fatti e le colonne di tipo di dati Date nella tabella relativa alla data.  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>Per specificare una tabella relativa alla data e un identificatore univoco  
  
1.  In Progettazione modelli fare clic sulla tabella relativa alla data.  
  
2.  Fare clic sul menu **Tabella** , selezionare **Data**, quindi scegliere **Contrassegna come tabella data**  
  
3.  Nella casella di riepilogo **Data** della finestra di dialogo **Contrassegna come tabella data** selezionare una colonna da utilizzare come identificatore univoco. In questa colonna devono essere inclusi valori univoci e il tipo di dati utilizzato deve essere Date. Ad esempio:   
  
    |date|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  Se necessario, creare tutte le relazioni tra le tabelle dei fatti e la tabella relativa alla data.  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli &#40;SSAS tabulare&#41;](calculations-ssas-tabular.md)   
 [Funzioni di Business Intelligence di tempo &#40;DAX&#41;](https://msdn.microsoft.com/library/ee634763.aspx)  
  
  
