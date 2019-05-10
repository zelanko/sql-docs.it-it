---
title: Per gli sviluppatori&#39;Guida (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f87f812ad9f4f12f5f78828e88c220e3dcf494d
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483032"
---
# <a name="developer39s-guide-master-data-services"></a>Per gli sviluppatori&#39;Guida (Master Data Services)
  Vengono fornite informazioni su come scrivere il codice per personalizzare la modalità di interazione degli utenti con [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Viene illustrato come:  
  
-   Scrivere un programma che acceda al servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Il servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] è un servizio di Windows Communication Foundation (WCF) che gli sviluppatori utilizzano per controllare le funzionalità di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] tramite codice.  
  
-   Incorporare le funzionalità di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in applicazioni esistenti.  
  
-   Scrivere il codice per eseguire azioni ripetitive o complesse che sono difficili o impossibili da eseguire con l'interfaccia utente di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   Creare un flusso di lavoro personalizzato eseguito in risposta a una regola business specificata. Un flusso di lavoro personalizzato chiama il codice scritto, che può eseguire qualsiasi azione richiesta per elaborare il flusso di lavoro.  
  
## <a name="master-data-manager-web-service"></a>Servizio Web Gestione dati master  
 Il servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] consente di utilizzare a livello di codice le caratteristiche di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] da qualsiasi computer che può accedere al sito Web di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Prima di iniziare a scrivere il codice per accedere al servizio Web, è necessario generare le classi proxy, che sono contenute in uno spazio dei nomi specificato dall'utente. Nella presente documentazione viene utilizzato <xref:Microsoft.MasterDataServices> come spazio dei nomi del proxy. La classe proxy principale utilizzata per eseguire le operazioni del servizio Web è la classe <xref:Microsoft.MasterDataServices.ServiceClient>, che implementa l'interfaccia <xref:Microsoft.MasterDataServices.IService>. Dal codice, chiamare i metodi della classe <xref:Microsoft.MasterDataServices.ServiceClient> per accedere al servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Il resto delle classi nello spazio dei nomi viene utilizzato dalle operazioni del servizio Web.  
  
### <a name="web-service-content"></a>Contenuto del servizio Web  
 [Creare le classi proxy del servizio Web Gestione dati master](create-master-data-manager-web-service-proxy-classes.md)  
 Viene descritto come abilitare la pubblicazione dei metadati dal sito Web di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e come creare le classi proxy che possono essere utilizzate per accedere a livello di programmazione alle operazioni del servizio Web.  
  
 [Operazioni del servizio Web per categoria &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
 Elenco per categoria delle operazioni del servizio Web della classe <xref:Microsoft.MasterDataServices.ServiceClient>.  
  
## <a name="custom-workflows"></a>Flussi di lavoro personalizzati  
 In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] vengono utilizzate le regole business per creare soluzioni di base per il flusso di lavoro. È possibile aggiornare e convalidare automaticamente i dati, nonché inviare notifiche mediante posta elettronica in base alle condizioni specificate. Le regole business in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] vengono utilizzate per gestire gli scenari di flussi di lavoro più comuni. Se il flusso di lavoro richiede l'elaborazione di eventi più complessi, ad esempio approvazioni multilivello o alberi delle decisioni complessi, è possibile configurare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in modo da inviare i dati a un assembly personalizzato creato. Per gestire i flussi di lavoro personalizzati, è necessario configurare e avviare SQL Server MDS Workflow Integration Service sul computer dell'applicazione Web e creare un assembly che implementi l'interfaccia <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>.  
  
### <a name="custom-workflow-content"></a>Contenuto del flusso di lavoro personalizzato  
 [Creare un flusso di lavoro personalizzato &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)  
 Istruzioni sulla creazione di un assembly del gestore dei flussi di lavoro, sulla configurazione e l'avvio di SQL Server MDS Workflow Integration Service e sulla creazione di una regola business in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] per avviare un flusso di lavoro personalizzato.  
  
## <a name="web-server-namespaces"></a>Spazi dei nomi del server Web  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] installa un set di assembly nel computer del server Web. Questi assembly contengono spazi dei nomi utilizzabili per scenari avanzati che consentono di personalizzare il comportamento del computer del server Web. Nella tabella seguente vengono descritti tali spazi dei nomi.  
  
|Spazio dei nomi|Descrizione|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|Contiene classi utilizzabili per creare un pacchetto di distribuzione da un modello e distribuire un pacchetto in un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|  
|<xref:Microsoft.MasterDataServices.Services>|Contiene una classe che riceve ed elabora operazioni del servizio Web eseguite sul computer del server Web tramite l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|Contiene classi che definiscono le modalità di passaggio dei dati dal computer client attraverso l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] al computer del server Web.|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|Contiene classi che definiscono le modalità di passaggio di richieste e risposte dal computer client attraverso l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] al computer del server Web.|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|Contiene l'interfaccia che definisce le operazioni che possono essere chiamate tramite il servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
  
  
