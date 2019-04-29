---
title: MSSQLSERVER_-1 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc558a0a0f5b8bd05f2ff461cc45a73aafa6da23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916398"
---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|-1|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Si è verificato un errore durante il tentativo di stabilire una connessione al server.  Quando ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questo errore potrebbe essere provocato dal fatto che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non ammette connessioni remote sotto le impostazioni predefinite. (provider: Interfacce di rete SQL, errore: 28 - il server non supporta il protocollo richiesto) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], errore: -1)|  
  
## <a name="explanation"></a>Spiegazione  
 Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. L'errore può essere causato da uno dei problemi seguenti:  
  
-   Un nome di istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato non è valido.  
  
-   Il protocollo TCP o i protocolli named pipe non sono abilitati.  
  
-   La connessione è stata rifiutata dal firewall del server.  
  
-   Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser (sqlbrowser) non è stato avviato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per risolvere l'errore, eseguire una delle operazioni seguenti:  
  
-   Controllare l'ortografia del nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato nella stringa di connessione.  
  
-   Usare lo strumento Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per consentire a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accettare le connessioni remote tramite protocolli TCP o Named Pipes.  
  
-   Assicurarsi di avere configurato il firewall nell'istanza server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per aprire porte per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la porta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser (UDP 1434).  
  
-   Assicurarsi che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sia stato avviato nel server.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un Firewall di Windows per l'accesso al motore di Database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurazione di protocolli Client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolli e librerie di rete](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configurazione di rete dei client](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurazione di protocolli Client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
