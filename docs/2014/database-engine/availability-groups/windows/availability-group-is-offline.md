---
title: Il gruppo di disponibilità è offline | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4b4946ebec1b9f66ba0a680e97b00cb185bc7e65
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937122"
---
# <a name="availability-group-is-offline"></a>Il gruppo di disponibilità è offline
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criterio**|Stato online del gruppo di disponibilità|  
|**Problema**|Il gruppo di disponibilità è offline.|  
|**Categoria**|**Critico**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Description  
 Questi criteri consentono di controllare lo stato online o offline del gruppo di disponibilità. I criteri si trovano in uno stato non integro e viene generato un avviso quando la risorsa cluster del gruppo di disponibilità è offline o nel gruppo di disponibilità non è disponibile una replica primaria.  
  
 I criteri si trovano in uno stato integro quando la risorsa cluster del gruppo di disponibilità è online e nel gruppo di disponibilità è disponibile una replica primaria.  
  
> [!NOTE]  
>   Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa alla situazione in cui il [gruppo di disponibilità è offline](https://go.microsoft.com/fwlink/p/?LinkId=220850) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 Questo problema può essere causato da un errore nell'istanza del server in cui è ospitata la replica primaria o dal passaggio alla modalità offline della risorsa del gruppo di disponibilità WSCF (Windows Server Failover Clustering). Di seguito sono riportate le possibili cause del passaggio alla modalità offline del gruppo di disponibilità:  
  
-   Il gruppo di disponibilità non è configurato con la modalità di failover automatico. La replica primaria non è più disponibile e il ruolo di tutte le repliche nel gruppo di disponibilità diventa RISOLUZIONE.  
  
    -   Il servizio dell'istanza della replica primaria non funziona o non risponde.  
  
    -   Si è verificato un problema di connettività tra il gruppo di disponibilità e il cluster.  
  
-   Il gruppo di disponibilità è configurato con la modalità di failover automatico, ma non viene completato correttamente.  
  
    -   Durante il failover automatico, il controllo di conformità della replica primaria nella replica di destinazione non viene eseguito correttamente e nessuna replica è disponibile a diventare la nuova primaria.  
  
-   La risorsa del gruppo di disponibilità nel cluster passa alla modalità offline.  
  
    -   Si verifica un problema grave in qualsiasi risorsa cluster dipendente che ne determina il passaggio alla modalità offline. La risorsa del gruppo di disponibilità è offline finché la risorsa dipendente non passa alla modalità online.  
  
    -   Un problema grave nel cluster determina la disabilitazione della risorsa del gruppo di disponibilità.  
  
-   È in corso un failover automatico, manuale o forzato per il gruppo di disponibilità.  
  
## <a name="possible-solutions"></a>Possibili soluzioni  
 Di seguito sono riportate le possibili soluzioni a questo problema:  
  
-   Se l'istanza di SQL Server della replica primaria non è attiva, riavviare il server, quindi verificare che venga recuperato uno stato integro per il gruppo di disponibilità.  
  
-   Se sembra che il failover automatico non sia stato completato correttamente, verificare che i database della replica siano sincronizzati con la replica primaria nota in precedenza, quindi eseguire il failover alla replica primaria. Se i database non sono sincronizzati, selezionare una replica con una perdita minima di dati, quindi recuperare alla modalità failover.  
  
-   Se la risorsa nel cluster è offline mentre le istanze di SQL Server sembrano essere integre, utilizzare Gestione cluster di failover per controllare l'integrità del cluster o altri problemi del cluster nel server. Gestione cluster di failover può essere utilizzato anche per tentare di portare online la risorsa del gruppo di disponibilità.  
  
-   Se è in corso un failover, attenderne il completamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
