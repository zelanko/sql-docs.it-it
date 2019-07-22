---
title: Configurare i criteri di integrità (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c59138d5d1f06ffee0266f9e97d5faf46ef28f08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115435"
---
# <a name="configure-health-policies-sql-server-utility"></a>Configurazione dei criteri di integrità (Utilità SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Usare il dashboard di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare i parametri delle risorse di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni livello dati. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Per visualizzare i risultati dei criteri di integrità di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , connettersi a un punto di controllo dell'utilità da [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per altre informazioni, vedere [Utilizzo di Esplora utilità per gestire Utilità SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] È possibile configurare i criteri di integrità di Utilità per applicazioni livello dati e istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I criteri di integrità possono essere definiti a livello globale per tutte le applicazioni livello dati e per tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure possono essere definiti singolarmente per ogni applicazione livello dati e per ogni istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>Criteri di monitoraggio per le applicazioni del livello dati  
 Di seguito vengono indicati i criteri di sovrautilizzo e sottoutilizzo per le applicazioni livello dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Utilizzo del processore da parte dell'applicazione del livello dati.  
  
-   Spazio occupato dall'applicazione del livello dati per i file di database.  
  
-   Spazio occupato dall'applicazione del livello dati per i volumi di archiviazione.  
  
-   Utilizzo del processore del computer.  
  
> [!NOTE]  
>  Utilizzo del volume di archiviazione e del processore sono criteri di sola lettura per le applicazioni livello dati.  
  
 Per altre informazioni sulla visualizzazione o sulla modifica di criteri di monitoraggio globali per le applicazioni livello dati, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Per altre informazioni sulla visualizzazione o sulla modifica di criteri di monitoraggio per singole applicazioni livello dati, vedere [Dettagli di Applicazioni di livello dati distribuite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>Criteri di monitoraggio per le istanze gestite di SQL Server  
 I criteri di sovrautilizzo e sottoutilizzo per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono i seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i file di database.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i volumi di archiviazione.  
  
-   Utilizzo del processore del computer.  
  
 Per altre informazioni sulla visualizzazione o sulla modifica di criteri di monitoraggio globali per le istanze globali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Per altre informazioni sulla visualizzazione o sulla modifica di criteri di monitoraggio per singole istanze globali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Riduzione delle segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
