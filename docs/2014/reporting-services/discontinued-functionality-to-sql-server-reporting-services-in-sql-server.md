---
title: Funzionalità non più supportate
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8cdec8ed3fbdd539b0c630af2a298ebf9807d6a7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755759"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>Funzionalità non più supportate in SQL Server Reporting Services (SSRS)

  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non più disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Non sono inclusi avvisi relativi al supporto non più disponibile per versioni specifiche del sistema operativo o per [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS). Per ulteriori informazioni sui prerequisiti di sistema, vedere [requisiti hardware e software per l'installazione di SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 In questo argomento  
  
- [SQL Server 2014 Reporting Services funzionalità non più supportate](#bkmk_sql14)  
  
- [Funzionalità deprecate in SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
- [Funzionalità deprecate in SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-discontinued-functionality"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Reporting Services funzionalità sospesa

 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono presenti funzionalità di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]non più disponibili.  
  
##  <a name="sssql11-reporting-services-discontinued-functionality"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Reporting Services funzionalità sospesa

 In questa sezione vengono descritte le funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non più disponibili in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono presenti funzionalità di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]non più disponibili.  
  
##  <a name="sql-server-2008-r2-reporting-services-discontinued-functionality"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services funzionalità non più disponibili

 In questa sezione vengono descritte le funzionalità non più disponibili in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
> Poiché SQL Server 2008 R2 è un aggiornamento secondario della versione di SQL Server 2008, è consigliabile rivedere anche il contenuto nella sezione relativa a SQL Server 2008.
  
### <a name="64-bit-platform-support"></a>Supporto della piattaforma a 64 bit

 A partire da [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], il componente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non supporta più server basati su Itanium che eseguono Windows Server 2003 o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a supportare altri sistemi operativi a 64 bit, tra cui Windows Server 2008 e Windows Server 2008 R2 per sistemi basati su Itanium. Per eseguire l'aggiornamento a [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] da un'installazione di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in un'edizione del sistema basata su Itanium di Windows Server 2003 o Windows Server 2003 R2, è necessario prima aggiornare il sistema operativo.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenziali dell'origine dati nell'accesso a URL

 Le stringhe dei parametri di accesso con URL *DSU: DataSourceName = value* e *DSP: DataSourceName = value* sono ora sospese. Nelle versioni precedenti queste stringhe di parametri sono archiviate in testo normale nella cache del browser e non viene pertanto garantita la sicurezza.  
  
## <a name="next-steps"></a>Passaggi successivi

 - [Novità &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [Modifiche del comportamento di SQL Server Reporting Services in SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [Funzionalità deprecate di SQL Server Reporting Services in SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)