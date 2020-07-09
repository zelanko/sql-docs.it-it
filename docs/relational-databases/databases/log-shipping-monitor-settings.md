---
title: Impostazioni monitoraggio log shipping | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: b4ff8d6e7348ece5f09f9ac529c474a302e30be7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726442"
---
# <a name="log-shipping-monitor-settings"></a>Impostazioni monitoraggio log shipping
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare questa pagina per configurare e modificare le proprietà del server di monitoraggio del log shipping.  
  
 Per approfondimenti sui concetti correlati al log shipping, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Istanza server di monitoraggio**  
 Visualizza il nome dell'istanza del server attualmente configurato come server di monitoraggio per la configurazione per il log shipping.  
  
 **Connettere**  
 Consente di scegliere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare come server di monitoraggio e di connettersi a tale istanza. È necessario che l'account utilizzato per la connessione sia membro del ruolo predefinito del server sysadmin nell'istanza del server secondario.  
  
 **Tramite rappresentazione dell'account proxy del processo**  
 Consente al log shipping di rappresentare l'account proxy di SQL Server Agent durante la connessione all'istanza del server di monitoraggio. Per aggiornare lo stato delle operazioni di log shipping i processi di backup, di copia e di ripristino devono potersi connettere al server di monitoraggio.  
  
 **Tramite l'account di accesso di SQL Server seguente**  
 Consente al log shipping di utilizzare un account di accesso specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la connessione all'istanza del server di monitoraggio. Per aggiornare lo stato delle operazioni di log shipping i processi di backup, di copia e di ripristino devono potersi connettere al server di monitoraggio. Se si desidera che il log shipping utilizzi un account di accesso specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare questa opzione e quindi specificare l'account di accesso e la password.  
  
 **Elimina cronologia dopo**  
 Consente di specificare per quanto tempo le informazioni sulla cronologia di log shipping vengono mantenute sul server di monitoraggio prima di essere eliminate.  
  
 **Nome processo**  
 Indica il nome del processo di gestione degli avvisi di SQL Server Agent utilizzato dal log shipping per generare avvisi in caso di superamento dei valori soglia per il backup o il ripristino. Al momento della prima creazione di tale processo è possibile modificarne il nome nell'apposita casella.  
  
 **Pianificare**  
 Indica la pianificazione corrente del processo di gestione degli avvisi di SQL Server Agent.  
  
 **Modifica**  
 Consente di modificare i parametri del processo di gestione degli avvisi di SQL Server Agent.  
  
 **Disabilita questo processo**  
 Consente di sospendere il processo di gestione degli avvisi di SQL Server Agent.  
  
  
