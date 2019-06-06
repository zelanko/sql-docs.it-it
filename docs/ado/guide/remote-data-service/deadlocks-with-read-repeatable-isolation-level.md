---
title: Deadlock con livello di isolamento Repeatable Read | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 51899f0c3b37cf8228bb25ae8183d8f8e27ba4e0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699512"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Deadlock con livello di isolamento di lettura ripetibile
Se un oggetto business personalizzato utilizza un livello di isolamento di lettura ripetibile per accedere a SQL Server e l'oggetto business è chiamato simultaneamente da due client che inviano una query e aggiornamento nella stessa transazione, è possibile un deadlock. Servizio dati remoto è progettato per consentire a uno dei processi di timeout per rilasciare il deadlock, ma l'aggiornamento avrà esito negativo per quel client.  
  
 Usare la [servizio cursore](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **Timeout comando** proprietà dinamica per modificare la durata del timeout.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



