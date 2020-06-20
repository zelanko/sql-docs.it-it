---
title: Modifica della protezione delle transazioni in una sessione di mirroring del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d8bc9d0fb639770d33507c29a6ec67f60bd0434a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934395"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Modifica della protezione delle transazioni in una sessione di mirroring del database (Transact-SQL)
  La protezione delle transazioni è l'attributo che controlla la modalità operativa della sessione. Il proprietario del database può tuttavia modificare in qualsiasi momento tale protezione. Per impostazione predefinita, il livello di protezione delle transazioni è impostato su FULL (modalità operativa sincrona).  
  
 Se la protezione delle transazioni viene disabilitata, la sessione passa alla modalità operativa asincrona che consente di ottimizzare le prestazioni. In caso di indisponibilità del server principale, il server mirror viene arrestato ma risulta disponibile come server di standby a caldo (warm standby). Per il failover è necessario forzare il servizio, pertanto potrebbero verificarsi perdite di dati.  
  
### <a name="to-turn-on-transaction-safety"></a>Per attivare la protezione delle transazioni  
  
1.  Connettersi al server principale.  
  
2.  Eseguire l'istruzione Transact-SQL seguente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     dove *\<database>* è il nome del database con mirroring.  
  
### <a name="to-turn-off-transaction-safety"></a>Per disabilitare la protezione delle transazioni  
  
1.  Connettersi al server principale.  
  
2.  Eseguire l'istruzione seguente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     dove *\<database>* è il database con mirroring.  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Modalità di funzionamento del mirroring del database](database-mirroring-operating-modes.md)  
  
  
