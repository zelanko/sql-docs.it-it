---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fbe1fbc9aee04353ee4b5628ec1bddb7fc860a33
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553406"
---
# <a name="mssqlserver_233"></a>MSSQLSERVER_233
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|233|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|La connessione al server è stata stabilita con esito positivo, ma si è verificato un errore durante il processo di accesso. (provider: Provider memoria condivisa, errore: 0 - Nessun altro processo all'altra estremità della pipe.) (Microsoft SQL Server, Errore: 233)|  
  
## <a name="explanation"></a>Spiegazione  
 Non è possibile stabilire la connessione tra il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server. Questo errore potrebbe verificarsi poiché il server non è configurato per l'accettazione di connessioni remote.  
  
## <a name="user-action"></a>Azione dell'utente  
 Utilizzare lo strumento Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per consentire l'accettazione di connessioni remote in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Protocolli di rete e librerie di rete](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configurazione di rete dei client](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurare i protocolli client](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
