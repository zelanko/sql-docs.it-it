---
title: Opzione di configurazione del server remote admin connections | Microsoft Docs
description: Informazioni sul modo in cui le applicazioni nei computer remoti possono usare la connessione amministrativa dedicata (DAC). Per attivare questa funzionalità, vedere come usare l'opzione "remote admin connections" con "sp_configure".
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d7aa4d4b6658461be3a4fc5c762b3cef5343be4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651725"
---
# <a name="remote-admin-connections-server-configuration-option"></a>Opzione di configurazione del server remote admin connections
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre una connessione amministrativa dedicata (DAC). Questa connessione consente agli amministratori di accedere a un server in esecuzione per eseguire funzioni diagnostiche o istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , nonché di risolvere i problemi che si verificano nel server, anche quando il server è bloccato o è in esecuzione in uno stato anomalo e non risponde a una connessione del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Per impostazione predefinita, la connessione DAC è disponibile solo da un client nel server. Per consentire alle applicazioni client nei computer remoti di utilizzare la connessione DAC, utilizzare l'opzione remote admin connections di sp_configure.  
  
 Per impostazione predefinita, la connessione DAC è in attesa sull'indirizzo IP di loopback (127.0.0.1), porta 1434. Se la porta TCP 1434 non è disponibile, all'avvio di [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene assegnata dinamicamente una porta TCP. Quando in un computer sono installate più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verificare il numero della porta TCP nel log degli errori.  
  
 Nella tabella seguente sono elencati i valori possibili per l'opzione remote admin connections.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|Indica che l'utilizzo della connessione DAC è consentito solo alle connessioni locali.|  
|1|Indica che l'utilizzo della connessione DAC è consentito alle connessioni remote.|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene abilitata la connessione DAC da un computer remoto.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
