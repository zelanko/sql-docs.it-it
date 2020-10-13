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
ms.openlocfilehash: a3ec26ba8988f36e3deac88373a932ef377f8d59
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810031"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Visualizzazione dei risultati dei criteri di integrità delle risorse (Utilità SQL Server)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Usare il dashboard Utilità in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare i parametri delle risorse di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni livello dati. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>Visualizzare i risultati dei criteri di integrità delle risorse di Utilità SQL Server.  

1. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) selezionare **Visualizza**, quindi **Esplora utilità** per visualizzare il riquadro di spostamento di Esplora utilità. Per visualizzare il riquadro del contenuto, selezionare **Visualizza**, quindi selezionare **Contenuto Esplora utilità**.  

2. Nel riquadro di spostamento selezionare ![Connetti a utilità](../../relational-databases/manage/media/connect-to-utility.gif "Connetti a utilità")**Connetti a utilità**. Se non è stato creato un punto di controllo dell'utilità o se non sono state registrate istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o applicazioni livello dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

3. Selezionare il nodo del punto di controllo dell'utilità per visualizzare dati riepilogativi per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni livello dati (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati del dashboard vengono visualizzati nel riquadro del contenuto.  

4. Selezionare il nodo **Istanze gestite** per visualizzare i dati della visualizzazione elenco per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati della visualizzazione elenco vengono visualizzati nel riquadro del contenuto.  

5. Selezionare il nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) per visualizzare i dati della visualizzazione elenco per le applicazioni del livello dati (fare clic con il pulsante destro del mouse per aggiornare i dati). I dati della visualizzazione elenco vengono visualizzati nel riquadro del contenuto.  

## <a name="see-also"></a>Vedere anche

- [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [Riduzione delle segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [Dettagli delle applicazioni livello dati distribuite &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))
- [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](./utility-explorer-f1-help.md)
- [Amministrazione utilità &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))