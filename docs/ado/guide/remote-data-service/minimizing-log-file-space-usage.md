---
title: Riducendo al minimo utilizzo spazio File di Log | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1c6894a19c39df171dea3b621773daf31971895f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704263"
---
# <a name="minimizing-log-file-space-usage"></a>Riduzione al minimo dell'utilizzo dello spazio per il file di log
Un file di log può riempirsi rapidamente (sospendendo il server) se è presente un volume elevato di attività in un database di SQL Server. È possibile impostare il file di log **Truncate sul Checkpoint** estendere in modo significativo la durata del file di log per un database.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Per abilitare troncare in corrispondenza del Checkpoint in Microsoft SQL Server 6.5  
  
1.  Avviare Microsoft SQL Server Enterprise Manager, aprire l'albero per il Server e quindi aprire l'albero di dispositivi di Database.  
  
2.  Fare doppio clic il nome del database in cui questa funzionalità verrà abilitata.  
  
3.  Dal **Database** scheda, seleziona **Truncate**.  
  
4.  Dal **le opzioni** scheda, seleziona **troncare Log in corrispondenza del Checkpoint**e quindi fare clic su **OK**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Per abilitare troncare in corrispondenza del Checkpoint in Microsoft SQL Server 7.0  
  
1.  Avviare Microsoft SQL Server Enterprise Manager, aprire l'albero per il Server e quindi aprire la struttura di database.  
  
2.  Fare doppio clic il nome del database in cui questa funzionalità verrà abilitata e scegliere **proprietà**.  
  
3.  Dal **le opzioni** scheda, seleziona **troncare Log in corrispondenza del Checkpoint**e quindi fare clic su **OK**.  
  
 Per altre informazioni sul **Truncate sul Checkpoint** delle funzionalità, vedere la documentazione di Microsoft SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


