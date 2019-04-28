---
title: Uso forzato del servizio in una sessione di mirroring del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- forced service [SQL Server]
- database mirroring [SQL Server], forcing service
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ef1a7101a0bd16c3ee2868f47a8dc15f29092621
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806713"
---
# <a name="force-service-in-a-database-mirroring-session-transact-sql"></a>Utilizzo forzato del servizio in una sessione di mirroring del database (Transact-SQL)
  Nella modalità a prestazioni elevate e in quella a sicurezza elevata senza failover automatico, se si verifica un errore nel server principale mentre è disponibile il server mirror, il proprietario del database può rendere disponibile il database forzando il failover del servizio nel database mirror, sebbene tale operazione implichi la possibile perdita di dati. Questa opzione è disponibile esclusivamente nelle condizioni seguenti:  
  
-   Il server principale non è disponibile.  
  
-   WITNESS è impostato su OFF o connesso al server mirror.  
  
> [!CAUTION]  
>  Il servizio forzato rappresenta esclusivamente un metodo di ripristino di emergenza. L'utilizzo forzato del servizio può implicare perdite di dati. È quindi consigliabile forzare il servizio solo se si è consapevoli che il ripristino immediato del servizio nel database può causare perdite di dati. Se l'utilizzo forzato del servizio implica il rischio della perdita di dati importanti, è consigliabile arrestare il mirroring e risincronizzare manualmente i database. Per altre informazioni sui rischi dell'uso forzato del servizio, vedere [Modalità di funzionamento del mirroring del database](database-mirroring-operating-modes.md).  
  
 L'utilizzo forzato del servizio comporta l'interruzione della sessione e l'avvio di un nuovo fork di recupero. L'effetto dell'utilizzo forzato del servizio è simile alla rimozione del mirroring e al recupero del database principale precedente. Tuttavia, l'utilizzo forzato del servizio facilita la risincronizzazione dei database, con possibile perdita di dati, quando viene ripreso il mirroring.  
  
### <a name="to-force-service-in-a-database-mirroring-session"></a>Per forzare il servizio in una sessione di mirroring del database  
  
1.  Connettersi al server mirror.  
  
2.  Eseguire l'istruzione seguente:  
  
     ALTER DATABASE *<nome_database>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     dove *<nome_database>* corrisponde al database con mirroring.  
  
     Il server mirror esegue immediatamente la transizione al server principale e il mirroring viene sospeso.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)  
  
  
