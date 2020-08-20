---
description: Topologie per la sincronizzazione tramite il Web
title: Topologie per la sincronizzazione tramite il Web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web synchronization, topologies
- IIS server configuration [SQL Server replication]
ms.assetid: 59444faf-bcb6-4421-a3df-8715753e453b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 287392a3328574c9c673c3b3ce04228e8b520654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455578"
---
# <a name="topologies-for-web-synchronization"></a>Topologie per la sincronizzazione tramite il Web
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile scegliere tra diverse topologie di replica di sincronizzazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite il Web. Le modalità comuni di configurazione della sincronizzazione tramite il Web includono:  
  
-   Server singolo  
  
-   Due server  
  
-   Più sistemi [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) e ripubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Per informazioni sulla configurazione della sincronizzazione Web, vedere [Configurare la sincronizzazione Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="single-server"></a>Server unico  
 Nella topologia più semplice, quella di tipo IIS, il server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono contenuti in un unico server. I Sottoscrittori si sincronizzano connettendosi ad IIS sul server di pubblicazione. Il server di pubblicazione può essere protetto da un firewall.  
  
> [!NOTE]  
>  L'uso di questa funzionalità è consigliabile solo per gli scenari intranet. Per gli altri scenari, è consigliabile che il server IIS e i server di pubblicazione e di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si trovino su computer diversi.  
  
 ![Sincronizzazione Web con un singolo server](../../relational-databases/replication/media/web-sync02.gif "Sincronizzazione Web con un singolo server")  
  
## <a name="two-servers"></a>Due server  
 È possibile posizionare IIS su un server e configurare il server di pubblicazione e quello di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su un altro server. Il server che esegue IIS può essere isolato da Internet da un firewall. I Sottoscrittori si sincronizzano connettendosi ad IIS.  
  
 ![Sincronizzazione Web con due server](../../relational-databases/replication/media/web-sync03.gif "Sincronizzazione Web con due server")  
  
## <a name="multiple-iis-systems-and-sql-server-republishing"></a>Più sistemi IIS e ripubblicazione SQL Server  
 Se è necessario supportare numeri molto elevati di Sottoscrittori che si sincronizzano contemporaneamente, è possibile suddividere il lavoro tra più computer che eseguono IIS.  
  
 ![Sincronizzazione Web con più server IIS](../../relational-databases/replication/media/web-sync04.gif "Sincronizzazione Web con più server IIS")  
  
 Se sul computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è richiesto un ulteriore bilanciamento del carico, è possibile creare una gerarchia di ripubblicazione su più computer. Il server di pubblicazione di livello massimo pubblica i dati nei Sottoscrittori che a loro volta ripubblicano i dati, richieste di bilanciamento del carico dei Sottoscrittori.  
  
> [!NOTE]  
>  I Sottoscrittori possono eseguire la sincronizzazione solo con un server di pubblicazione specifico. Un Sottoscrittore del server di ripubblicazione A, ad esempio, non potrà eseguire la sincronizzazione con il server di ripubblicazione B, se A non è disponibile.  
  
 ![Sincronizzazione Web con ripubblicazione](../../relational-databases/replication/media/web-sync05.gif "Sincronizzazione Web con ripubblicazione")  
  
## <a name="see-also"></a>Vedere anche  
 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)   
 [Sincronizzazione Web per la replica di tipo merge](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
