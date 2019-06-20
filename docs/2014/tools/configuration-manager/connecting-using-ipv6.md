---
title: Connessione con IPv6 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db26351430c6b7e0737273b2107bea242c455a2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253775"
---
# <a name="connecting-using-ipv6"></a>Connessione con IPv6
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supportano completamente sia IPv4 (protocollo IP versione 4) sia IPv6 (protocollo IP versione 6). Quando Windows è configurato in modo da utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]per IPv6 i componenti riconoscono automaticamente l'esistenza di IPv6. Non è necessaria alcuna configurazione particolare di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Il supporto include, tra l'altro, le caratteristiche seguenti:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e gli altri componenti server possono restare in ascolto contemporaneamente sugli indirizzi IPv4 e IPv6. Quando si utilizza sia IPv4 che IPv6, è possibile utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per configurare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] in modo che resti in ascolto solo sugli indirizzi di IPv4 o solo sugli indirizzi di IPv6.  
  
-   Quando il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser in esecuzione su un computer che supporta sia IPv4 che IPv6 riceve una richiesta su un indirizzo IPv4, risponde con un indirizzo IPv4 e con la prima porta TCP IPv4 in elenco. Quando riceve una richiesta su un indirizzo IPv6, il servizio risponde con un indirizzo IPv6 e con la prima porta TCP IPv6 in elenco. Per evitare inconsistenze, è consigliabile che i listener IPv4 e IPv6 siano configurati in modo da restare in ascolto sulla stessa porta.  
  
-   Strumenti quali [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accettano sia i formati IPv4 che IPv6 per gli indirizzi IP. Nella maggior parte dei casi non è necessario modificare la stringa di connessione se si specifica \<*nome_computer*>\\<*nome_istanza*> usando il nome host o il nome di dominio completo (FQDN) del server. Se nel computer server vengono utilizzati sia IPv4 che IPv6, il relativo nome host o FQDN verrà risolto in più indirizzi IP, tra cui almeno un indirizzo IPv4 e più indirizzi IPv6. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client tenta di stabilire le connessioni usando questi indirizzi IP nell'ordine in cui li ha ricevuti da TCP/IP e usa la prima connessione che ha esito positivo. Poiché l'ordine non può essere previsto da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, deve essere considerato come casuale. In presenza di indirizzi sia IPv4 che IPv6 vengono tentati prima gli indirizzi IPv4. Questa logica è trasparente agli utenti di ODBC, OLE DB o ADO.NET.  
  
    > [!NOTE]  
    >  Se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è in ascolto su IPv4, prima che venga tentata la connessione sull'indirizzo IPv6 si dovrà attendere il timeout della connessione IPv4. Per evitare tale attesa, stabilire direttamente una connessione all'indirizzo IP di IPv6 o configurare un alias sul client con l'indirizzo IPv6.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)  
  
  
