---
title: MSSQLSERVER_53 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "53"
helpviewer_keywords:
- 53 (Database Engine error)
ms.assetid: 1234f5a2-b3d1-425a-b29f-480fa792305f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 42b33ba09ee5ba1eb924b38fe0aa8a665fd88adb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68109617"
---
# <a name="mssqlserver_53"></a>MSSQLSERVER_53
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|53|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Si è verificato un errore durante il tentativo di stabilire una connessione al server.  Quando ci si connette a SQL Server, è possibile che l'errore sia determinato dal fatto che le impostazioni predefinite di SQL Server non consentono le connessioni remote. (provider: provider named pipe, errore: 40 - Impossibile aprire una connessione a SQL Server) (.Net SqlClient Data Provider)|  
  
## <a name="explanation"></a>Spiegazione  
Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. Questo errore potrebbe verificarsi poiché il client non è in grado di risolvere il nome del server oppure il nome del server non è corretto.  
  
## <a name="user-action"></a>Azione dell'utente  
Verificare di avere immesso il nome corretto del server sul client e che dal client sia possibile risolvere il nome del server. Per verificare la risoluzione dei nomi TCP/IP, con il sistema operativo Windows è possibile usare il comando **ping**.  
  
## <a name="see-also"></a>Vedere anche  
[Protocolli e librerie di rete](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configurazione di rete dei client](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurazione di protocolli client](~/database-engine/configure-windows/configure-client-protocols.md)  
[Abilitare o disabilitare un protocollo di rete del server](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
