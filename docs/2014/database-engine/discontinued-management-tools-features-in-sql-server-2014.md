---
title: Caratteristiche degli strumenti di gestione in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c966c3e4388588810438d7e91a9ae0356ef60c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780350"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>Funzionalità degli strumenti di gestione non più supportate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità degli strumenti di gestione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non più disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="features-removed-in-includesscurrentincludessscurrent-mdmd"></a>Funzionalità rimosse in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 None  
  
## <a name="features-removed-in-includesssql11includessssql11-mdmd"></a>Funzionalità rimosse in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 L'editor del codice di SQL Server Compact Edition è stato rimosso da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Il supporto per SQL Server Compact Edition è stato rimosso da Esplora oggetti, Esplora soluzioni ed Esplora modelli. Utilizzare invece gli editor Transact-SQL in Microsoft Visual Studio 2010 Service Pack 1 o Webmatrix.  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>Sottosistema ActiveX per SQL Server Agent  
 Il sottosistema ActiveX per SQL Server Agent è stato rimosso in questa versione. Non è disponibile alcuna funzionalità sostitutiva.  
  
### <a name="spaddtask-spdeletetask-spupdatetask"></a>sp_addtask, sp_deletetask, sp_updatetask  
 Sp_addtask, sp_deletetask e sp_updatetask sono state rimosse in questa versione. Non utilizzare questa funzionalità nelle applicazioni nuove o aggiornate.  
  
### <a name="net-send-and-pager-notification"></a>Notifica tramite Net Send e cercapersone  
 Le notifiche tramite Net Send e cercapersone sono state rimosse in questa versione. Non utilizzare questa funzionalità nelle applicazioni nuove o aggiornate.  
  
### <a name="data-tier-applications"></a>Applicazioni livello dati  
 Alcune funzionalità di applicazione livello dati (DAC) presenti in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] sono state rimosse in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Tuttavia, Data-Tier Application Framework (DACfx versione 3.0) rilasciato con [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] è compatibile con [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] tramite [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. DAC versione 3.0 non è supportato dalle versioni precedenti di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] incluso [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]. I progetti di database di Visual Studio 2010 non supportano i pacchetti DACPAC di applicazione livello dati 3.0 o i pacchetti di esportazione dell'applicazione livello dati (BACPAC) generati con DACfx versione 3.0 o successive.  
  
 È consigliabile utilizzare i progetti di database della versione disponibile più recente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
 L'API di DACfx 3.0 e gli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportano la lettura dei file DACPAC e BACPAC creati utilizzando gli strumenti e le versioni DACfx di versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , pertanto è possibile estrarre database nei file DACPAC da queste versioni e distribuirli nelle versioni supportate di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità con le versioni precedenti](../../2014/getting-started/backward-compatibility.md)  
  
  
