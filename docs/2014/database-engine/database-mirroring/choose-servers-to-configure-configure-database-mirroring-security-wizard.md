---
title: Selezione dei server da configurare (Configurazione guidata sicurezza mirroring del database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24e31e60f29970ca1d3a73d3a215447e9dd325bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807239"
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>Selezione dei server da configurare (Configurazione guidata sicurezza mirroring del database)
  Utilizzare questa pagina per specificare le istanze del server che si desidera configurare. Prima di proseguire con la procedura guidata è necessario selezionare almeno un'istanza del server.  
  
 Se si deseleziona la casella di controllo corrispondente a un'istanza del server, la procedura guidata non apporterà alcuna modifica a tale istanza. Verrà chiesto tuttavia di immettere informazioni sull'istanza, che verranno salvate come parte della configurazione delle altre istanze del server. Se ad esempio si deseleziona la casella di controllo corrispondente all'istanza del server di controllo del mirroring, la procedura guidata chiederà di immettere l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di controllo del mirroring, perché è necessario creare tale account di accesso come parte della configurazione di sicurezza salvata nelle istanze del server principale e del server mirror.  
  
 **Per configurare il mirroring del database tramite SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Istanza server principale**  
 Consente di configurare la sicurezza per il server principale.  
  
 **Istanza server mirror**  
 Consente di configurare la sicurezza per il server mirror.  
  
 **Istanza server di controllo del mirroring**  
 Consente di configurare la sicurezza per il server di controllo del mirroring, se presente.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del database &#40;Pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
