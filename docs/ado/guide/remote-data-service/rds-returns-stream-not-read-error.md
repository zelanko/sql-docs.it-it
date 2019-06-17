---
title: Servizi Desktop remoto restituisce &quot;Stream non lettura&quot; errore | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 598326335c32f18b5d7f5a764d387e5b5ea536f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699422"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>Servizi Desktop remoto restituisce &quot;Stream non lettura&quot; errore
"L'oggetto Stream è stato possibile leggere in quanto è vuoto o la posizione corrente è alla fine della finestra di Stream. Per i flussi non vuoto, impostare la posizione corrente con la proprietà Position. Per determinare se un Stream è vuoto, controllare la proprietà della dimensione."  
  
 Se viene visualizzato questo messaggio di errore, si è tentato di utilizzare una query con parametri gerarchica su http. Servizi Desktop remoto non consente di utilizzare remote gerarchie con parametri.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


