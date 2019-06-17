---
title: Integration Services (SSIS) in un cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b70dbab14424335fe210f5a9b1ddbdbda4f90deb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889304"
---
# <a name="integration-services-ssis-in-a-cluster"></a>Integration Services (SSIS) in un cluster
  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] il clustering non è consigliato, poiché il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non è un servizio cluster o compatibile con i cluster né supporta il failover tra nodi del cluster. In un ambiente cluster è pertanto necessario installare e avviare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come servizio autonomo in ogni nodo del cluster.  
  
 Sebbene il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non sia un servizio cluster, è possibile configurarlo manualmente come risorsa cluster dopo l'installazione separata di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster.  
  
 Se tuttavia la disponibilità elevata rappresenta l'obiettivo della configurazione di un ambiente hardware cluster, è consigliabile evitare di configurare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster.  Per gestire i pacchetti in qualsiasi nodo del cluster da qualsiasi altro nodo del cluster, modificare il file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster. I file di configurazione devono essere modificati in modo da puntare a tutte le istanze disponibili di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui sono archiviati i pacchetti. Questa soluzione garantisce l'elevata disponibilità di cui necessita la maggior parte degli utenti, senza i problemi potenziali riscontrati quando il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è configurato come risorsa cluster. Per altre informazioni su come modificare il file di configurazione, vedere [Configurazione del servizio Integration Services &#40;SSIS&#41;](integration-services-service-ssis-service.md).  
  
 Per prendere decisioni appropriate sulla configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un ambiente cluster, è importante comprendere il ruolo di tale servizio. Per altre informazioni, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](integration-services-service-ssis-service.md).  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Informazioni sugli svantaggi della configurazione di Integration Services come risorsa cluster  
 Tra i potenziali svantaggi della configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster sono inclusi i seguenti:  
  
-   In caso failover, i pacchetti in esecuzione non si riavviano. È possibile risolvere gli errori relativi ai pacchetti riavviando i pacchetti dai checkpoint. È possibile eseguire il riavvio dai checkpoint senza configurare il servizio come risorsa cluster. Per ulteriori informazioni, vedere [Riavvio dei pacchetti tramite checkpoint](../packages/restart-packages-by-using-checkpoints.md).  
  
-   Quando si configura il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un gruppo di risorse diverso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non è possibile utilizzare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dai computer client per gestire i pacchetti archiviati nel database msdb. Tramite il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non possono essere delegate le credenziali in questo scenario a doppio hop.  
  
-   Quando sono presenti più gruppi di risorse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che includono il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un cluster, un failover potrebbe provocare risultati imprevisti. Si consideri lo scenario seguente. Il Gruppo 1, che include il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è in esecuzione nel Nodo A. Il Gruppo 2, che come il Gruppo 1 include il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è in esecuzione nel Nodo B. Si verifica il failover del Gruppo 2 nel Nodo A. Il tentativo di avviare un'altra istanza del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Nodo A ha esito negativo in quanto il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un servizio a istanza singola. L'esito del tentativo di failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel Nodo A dipende dalla configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Gruppo 2. Se il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è stato configurato in modo da influire sugli altri servizi nel gruppo di risorse, il failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha esito negativo a causa dell'errore del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se il servizio è stato configurato per non influire sugli altri servizi nel gruppo di risorse, verrà eseguito il failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel Nodo A. A meno che il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Gruppo 2 non sia stato configurato in modo da non influire sugli altri servizi nel gruppo di risorse, l'errore di failover del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può provocare anche un errore di failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Attività correlate  
 Per istruzioni dettagliate sulla configurazione del servizio Integration Services in un cluster, vedere [Configurazione del servizio Integration Services come risorsa cluster](../configure-the-integration-services-service-as-a-cluster-resource.md).  
  
  
