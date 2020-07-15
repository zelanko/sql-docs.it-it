---
title: Visualizzare i risultati dei criteri di integrità delle risorse (Utilità SQL Server) | Microsoft Docs
description: Informazioni su come usare SQL Server Management Studio per visualizzare i risultati dei criteri di integrità delle risorse di Utilità SQL Server per le istanze di SQL Server e delle applicazioni livello dati.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3f6397ebab2f53ebb37c54df20313926ebc84e68
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650780"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Visualizzazione dei risultati dei criteri di integrità delle risorse (Utilità SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Usare il dashboard Utilità in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare i parametri delle risorse di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni livello dati. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>Visualizzare i risultati dei criteri di integrità delle risorse di Utilità SQL Server.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) fare clic su **Visualizza**, quindi su **Esplora utilità** per visualizzare il riquadro di spostamento di Esplora utilità. Per visualizzare il riquadro del contenuto, fare clic su **Visualizza**, quindi su **Contenuto Esplora utilità**.  
  
2.  Nel riquadro di spostamento fare clic su ![](../../relational-databases/manage/media/connect-to-utility.gif "Connetti a utilità")**Connetti a utilità**. Se non è stato creato un punto di controllo dell'utilità o se non sono state registrate istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o applicazioni livello dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
3.  Fare clic sul nodo del punto di controllo dell'utilità per visualizzare dati riepilogativi per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni livello dati (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati del dashboard vengono visualizzati nel riquadro del contenuto.  
  
4.  Fare clic sul nodo **Istanze gestite** per visualizzare i dati della visualizzazione elenco per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati della visualizzazione elenco vengono visualizzati nel riquadro del contenuto.  
  
5.  Fare clic sul nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) per visualizzare i dati della visualizzazione elenco per le applicazioni del livello dati (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati della visualizzazione elenco vengono visualizzati nel riquadro del contenuto.  

## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [Dettagli di applicazioni livello dati distribuite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [Amministrazione utilità &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  
