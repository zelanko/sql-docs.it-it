---
title: Log di diagnostica dell'integrità dei gruppi di disponibilità Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c9a41540e9617f9eb9543677c9982b8bbb5985c3
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405008"
---
# <a name="always-on-availability-groups-health-diagnostics-log"></a>Log di diagnostica dell'integrità dei gruppi di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per monitorare l'integrità della replica di disponibilità primaria, la DLL risorse SQL Server eseguita dal cluster WSFC (Windows Server Failover Clustering) utilizza una stored procedure nell'istanza di SQL Server denominata [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).  
  
 La DLL risorse SQL Server mantiene aperta una connessione dedicata con l'istanza di SQL Server tramite la quale l'istanza di SQL Server invia periodicamente dati di diagnostica dell'integrità dettagliati alla DLL risorse SQL Server. I dati di diagnostica dell'integrità, insieme ai criteri di failover configurati nella risorsa gruppo di disponibilità del cluster (proprietà FailoverConditionLevel), vengono usati dal cluster per determinare se riavviare o eseguire il failover della risorsa del gruppo di disponibilità. Questa stored procedure rappresenta l'istanza "heartbeat" di SQL Server 2012 e superiore per il cluster WSFC, che è più granulare e affidabile rispetto a SQL Server 2008 R2 o inferiore, in cui viene effettuata una connessione periodica verso l'istanza con la query `SELECT @@SERVERNAME`. È quindi possibile controllare le condizioni che attivano i failover impostando la proprietà FailureConditonLevel per il gruppo di disponibilità.  
  
 **Utilizzare i log di diagnostica del cluster di failover SQL Server**
 
 Tutti i dati diagnostici dell'integrità che la DLL risorse SQL Server riceve da sp_server_diagnostics vengono salvati automaticamente nella directory Log predefinita dell'istanza di SQL Server (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log). Questi log sono noti come log SQLDIAG e vengono salvati in formato XEL (eventi estesi). I file nella directory Log di SQL Server hanno il seguente formato: \<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel. Osservando i log SQLDIAG può essere possibile determinare la causa principale dell'evento di failover o dell'errore risorsa del gruppo di disponibilità.  
  
 Per visualizzare un log SQLDIAG trascinare il file XEL in SQL Server Management Studio.  
  
  
