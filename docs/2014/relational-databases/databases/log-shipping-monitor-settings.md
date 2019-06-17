---
title: Impostazioni monitoraggio log shipping | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 788defce7f897e4da3a3680118c573b5a73ac3b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917054"
---
# <a name="log-shipping-monitor-settings"></a>Impostazioni monitoraggio log shipping
  Utilizzare questa pagina per configurare e modificare le proprietà del server di monitoraggio del log shipping.  
  
 Per approfondimenti sui concetti correlati al log shipping, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Istanza server di monitoraggio**  
 Visualizza il nome dell'istanza del server attualmente configurato come server di monitoraggio per la configurazione per il log shipping.  
  
 **Connect**  
 Consente di scegliere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare come server di monitoraggio e di connettersi a tale istanza. È necessario che l'account utilizzato per la connessione sia membro del ruolo predefinito del server sysadmin nell'istanza del server secondario.  
  
 **Tramite rappresentazione dell'account proxy del processo**  
 Consente al log shipping di rappresentare l'account proxy di SQL Server Agent durante la connessione all'istanza del server di monitoraggio. Per aggiornare lo stato delle operazioni di log shipping i processi di backup, di copia e di ripristino devono potersi connettere al server di monitoraggio.  
  
 **Tramite l'account di accesso di SQL Server seguente**  
 Consente al log shipping di utilizzare un account di accesso specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la connessione all'istanza del server di monitoraggio. Per aggiornare lo stato delle operazioni di log shipping i processi di backup, di copia e di ripristino devono potersi connettere al server di monitoraggio. Se si desidera che il log shipping utilizzi un account di accesso specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare questa opzione e quindi specificare l'account di accesso e la password.  
  
 **Elimina cronologia dopo**  
 Consente di specificare per quanto tempo le informazioni sulla cronologia di log shipping vengono mantenute sul server di monitoraggio prima di essere eliminate.  
  
 **Nome processo**  
 Indica il nome del processo di gestione degli avvisi di SQL Server Agent utilizzato dal log shipping per generare avvisi in caso di superamento dei valori soglia per il backup o il ripristino. Al momento della prima creazione di tale processo è possibile modificarne il nome nell'apposita casella.  
  
 **Pianificazione**  
 Indica la pianificazione corrente del processo di gestione degli avvisi di SQL Server Agent.  
  
 **Modifica**  
 Consente di modificare i parametri del processo di gestione degli avvisi di SQL Server Agent.  
  
 **Disabilita questo processo**  
 Consente di sospendere il processo di gestione degli avvisi di SQL Server Agent.  
  
  
