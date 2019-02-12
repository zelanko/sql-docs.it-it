---
title: 'Attività 5: Impostazione basate su termini relazioni | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 322c5a5afcd7c5d82982a86cb9398e66bb248c5d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034452"
---
# <a name="task-5-setting-term-based-relationships"></a>Attività 5: Impostazione delle relazioni basate su termini
  In questa attività, è definito alcune relazioni basate su termini per i valori per il **Supplier Name** dominio. Una relazione basata su termini consente di effettuare una correzione a un termine che fa parte di un valore in un dominio, consentendo in questo modo a più valori identici ad eccezione dell'ortografia di una parte in comune tra essi di essere considerati sinonimi identici. Ad esempio, **Inc** possono essere corretti per **Incorporated**. Queste relazioni vengono utilizzate da DQS nei processi di individuazione delle informazioni, di pulizia o di corrispondenza. Visualizzare [basate su termini creare relazioni](https://msdn.microsoft.com/library/hh510404.aspx) per altri dettagli.  
  
1.  Selezionare **Supplier Name** nel **elenco di domini**.  
  
2.  Passare al **relazioni basate su termini** scheda nel riquadro di destra.  
  
3.  Fare clic su **Aggiungi nuova relazione** pulsante sulla barra degli strumenti per aggiungere una relazione alla tabella.  
  
4.  Tipo **co** per il **valore** campo e **società** per il **Correggi in** campo.  
  
5.  Ripetere i due passaggi precedenti per i valori seguenti:  
  
    |Value|Correggi in|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relazioni basate su termini](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "relazioni basate su termini")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 6: Impostazione di sinonimi](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
