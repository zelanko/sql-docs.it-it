---
title: MSSQLSERVER_10060 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10060"
helpviewer_keywords:
- 10060 (Database Engine error)
ms.assetid: 28c21277-cad8-406c-a955-07933a56982a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee37bfd2c2ba17377589f8a3e744cc018b9d5775
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870788"
---
# <a name="mssqlserver10060"></a>MSSQLSERVER_10060
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10060|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Si è verificato un errore durante il tentativo di stabilire una connessione al server.  Quando ci si connette a SQL Server, è possibile che l'errore sia determinato dal fatto che le impostazioni predefinite di SQL Server non consentono le connessioni remote. (provider: provider TCP, errore: 0 - Impossibile stabilire la connessione. Risposta non corretta della parte connessa dopo l'intervallo di tempo oppure mancata risposta dall'host collegato.) (Microsoft SQL Server, Errore: 10060)|  
  
## <a name="explanation"></a>Spiegazione  
 Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. Questo errore potrebbe verificarsi poiché la connessione è stata rifiutata dal firewall del server oppure il server non è configurato per l'accettazione di connessioni remote.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per risolvere l'errore, eseguire una delle operazioni seguenti:  
  
-   Verificare che il firewall del computer sia configurato per consentire all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accettare le connessioni.  
  
-   Utilizzare lo strumento Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per consentire l'accettazione di connessioni remote in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un Firewall di Windows per l'accesso al motore di Database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurazione di protocolli Client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolli e librerie di rete](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configurazione di rete dei client](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurazione di protocolli Client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
