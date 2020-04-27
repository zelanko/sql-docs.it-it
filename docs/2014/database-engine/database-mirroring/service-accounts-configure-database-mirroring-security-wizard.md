---
title: Account di servizio (Configurazione guidata sicurezza mirroring del database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69877c6a20e37e012925185d0b807e9579066e35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754391"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Account di servizio (Configurazione guidata sicurezza mirroring del database)
  Quando si utilizza l'autenticazione di Windows, se le istanze del server utilizzano account diversi, specificare gli account di servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tali account di servizio devono essere tutti account di dominio negli stessi domini o in domini di tipo trusted.  
  
 Se tutte le istanze del server utilizzano lo stesso account di dominio oppure utilizzano l'autenticazione basata sui certificati, lasciare i campi vuoti. È sufficiente fare clic su **Fine**per configurare automaticamente gli account tramite la procedura guidata in base all'account della procedura guidata corrente.  
  
> [!IMPORTANT]  
>  Se gli endpoint del mirroring del database delle istanze del server sono configurati per l'utilizzo di certificati, è necessario lasciare vuoti tutti i campi degli account di servizio.  
  
 **Per configurare il mirroring del database tramite SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Principale**  
 Consente di specificare l'account di servizio dell'istanza del server principale. Immettere il nome di dominio in lettere maiuscole:  
  
 *DOMAINNAME*Nome utente NomeDominio*username* \\  
  
 **Mirror**  
 Consente di specificare l'account di servizio dell'istanza del server mirror. Immettere il nome di dominio in lettere maiuscole:  
  
 *DOMAINNAME*Nome utente NomeDominio*username* \\  
  
 **Controllo**  
 Consente di specificare l'account di servizio dell'istanza del server di controllo del mirroring. Immettere il nome di dominio in lettere maiuscole:  
  
 *DOMAINNAME*Nome utente NomeDominio*username* \\  
  
## <a name="see-also"></a>Vedi anche  
 [Proprietà database &#40;pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Avvia Monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [&#40;SQL Server di mirroring del database&#41;](database-mirroring-sql-server.md)   
 [Configurare gli account di accesso per il mirroring del database o Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
