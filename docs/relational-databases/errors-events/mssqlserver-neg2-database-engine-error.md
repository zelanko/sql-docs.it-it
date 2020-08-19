---
description: MSSQLSERVER_-2
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
ms.openlocfilehash: 9770367029f0399ebfb3f47cdd931096293469a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428563"
---
# <a name="mssqlserver_-2"></a>MSSQLSERVER_-2
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
