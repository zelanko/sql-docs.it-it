---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "-2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 09a5cbc03debdb4fc87986111fb0ac69138715bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903758"
---
# <a name="mssqlserver-2"></a>MSSQLSERVER_-2
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|-2|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Timeout.  Il tempo disponibile è scaduto prima del completamento dell'operazione o il server non risponde. (Microsoft SQL Server, Errore: -2)|  
  
## <a name="explanation"></a>Spiegazione  
Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. Questo errore potrebbe verificarsi poiché la connessione è stata rifiutata dal firewall del server.  
  
## <a name="user-action"></a>Azione dell'utente  
Verificare che il firewall dell'istanza del server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia configurato per l'accettazione delle connessioni.  
  
## <a name="see-also"></a>Vedere anche  
[Configurare Windows Firewall per consentire l'accesso a SQL Server](~/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
[Configurare Windows Firewall per l'accesso al motore di database](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[Configurazione di protocolli client](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolli e librerie di rete](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configurazione di rete dei client](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurazione di protocolli client](~/database-engine/configure-windows/configure-client-protocols.md)  
[Abilitare o disabilitare un protocollo di rete del server](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
