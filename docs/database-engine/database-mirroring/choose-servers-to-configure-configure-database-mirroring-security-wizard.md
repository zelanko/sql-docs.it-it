---
title: Selezione dei server da configurare (Configurazione guidata sicurezza mirroring del database) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e97c918af264b2628b77bbd5d31958aea5c5d978
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952051"
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>Selezione dei server da configurare (Configurazione guidata sicurezza mirroring del database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa pagina per specificare le istanze del server che si desidera configurare. Prima di proseguire con la procedura guidata è necessario selezionare almeno un'istanza del server.  
  
 Se si deseleziona la casella di controllo corrispondente a un'istanza del server, la procedura guidata non apporterà alcuna modifica a tale istanza. Verrà chiesto tuttavia di immettere informazioni sull'istanza, che verranno salvate come parte della configurazione delle altre istanze del server. Se ad esempio si deseleziona la casella di controllo corrispondente all'istanza del server di controllo del mirroring, la procedura guidata chiederà di immettere l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di controllo del mirroring, perché è necessario creare tale account di accesso come parte della configurazione di sicurezza salvata nelle istanze del server principale e del server mirror.  
  
 **Per configurare il mirroring del database tramite SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Istanza server principale**  
 Consente di configurare la sicurezza per il server principale.  
  
 **Istanza server mirror**  
 Consente di configurare la sicurezza per il server mirror.  
  
 **Istanza server di controllo del mirroring**  
 Consente di configurare la sicurezza per il server di controllo del mirroring, se presente.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del database &#40;Pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
