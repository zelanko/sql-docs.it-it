---
title: RDS restituisce &quot;un errore di&quot; lettura del flusso | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c89756e86a702217d5d9d8495bf62b0d27f52321
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922465"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS restituisce &quot;un errore di&quot; lettura del flusso
"Impossibile leggere l'oggetto flusso perché è vuoto o la posizione corrente si trova alla fine del flusso. Per i flussi non vuoti, impostare la posizione corrente con la proprietà Position. Per determinare se un flusso è vuoto, controllare la proprietà Size ".  
  
 Se viene visualizzato questo messaggio di errore, è possibile che si sia tentato di usare una query gerarchica con parametri su http. RDS non consente di utilizzare gerarchie con parametri remoti.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


