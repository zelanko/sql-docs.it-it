---
title: MSSQLSERVER_53 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "53"
helpviewer_keywords:
- 53 (Database Engine error)
ms.assetid: 1234f5a2-b3d1-425a-b29f-480fa792305f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1607d1b6122c4a703ee93cd17705807626e2f0db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867753"
---
# <a name="mssqlserver53"></a>MSSQLSERVER_53
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|53|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Si è verificato un errore durante il tentativo di stabilire una connessione al server.  Quando ci si connette a SQL Server, è possibile che l'errore sia determinato dal fatto che le impostazioni predefinite di SQL Server non consentono le connessioni remote. (provider: Provider named pipe, errore: 40 - Impossibile aprire una connessione a SQL Server) (.Net SqlClient Data Provider)|  
  
## <a name="explanation"></a>Spiegazione  
 Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. Questo errore potrebbe verificarsi poiché il client non è in grado di risolvere il nome del server oppure il nome del server non è corretto.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare di avere immesso il nome corretto del server sul client e che dal client sia possibile risolvere il nome del server. Per verificare la risoluzione dei nomi TCP/IP, con il sistema operativo Windows è possibile usare il comando **ping**.  
  
## <a name="see-also"></a>Vedere anche  
 [Protocolli e librerie di rete](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configurazione di rete dei client](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurazione di protocolli Client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
