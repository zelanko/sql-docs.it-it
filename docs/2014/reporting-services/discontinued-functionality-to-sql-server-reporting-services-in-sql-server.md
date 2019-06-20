---
title: Funzionalità non più supportate
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services-2014, sql-server-2014
ms.reviewer: ''
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 3a5472859c582e026fc0c5aafac21abccdc93044
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63165352"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>Funzionalità non più supportate in SQL Server Reporting Services (SSRS)

  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non più disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Non sono inclusi avvisi relativi al supporto non più disponibile per versioni specifiche del sistema operativo o per [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS). Per altre informazioni sui prerequisiti di sistema, vedere [Hardware and Software Requirements for Installing SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Contenuto dell'argomento:  
  
- [Funzionalità deprecate in SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
- [Funzionalità deprecate in SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
- [Funzionalità deprecate in SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services non più disponibile la funzionalità

 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono presenti funzionalità di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]non più disponibili.  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services non più disponibile la funzionalità

 In questa sezione vengono descritte le funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non più disponibili in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono presenti funzionalità di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]non più disponibili.  
  
##  <a name="bkmk_kj"></a> Funzionalità deprecate in SQL Server 2008 R2 Reporting Services

 In questa sezione vengono descritte le funzionalità non più utilizzate in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
> Poiché SQL Server 2008 R2 è un aggiornamento secondario della versione di SQL Server 2008, è consigliabile rivedere anche il contenuto nella sezione relativa a SQL Server 2008.
  
### <a name="64-bit-platform-support"></a>Supporto della piattaforma a 64 bit

 A partire da [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], il componente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non supporta più server basati su Itanium che eseguono Windows Server 2003 o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a supportare altri sistemi operativi a 64 bit, ad esempio Windows Server°2008 per sistemi basati su Itanium e Windows Server 2008 R2 per sistemi basati su Itanium. Per eseguire l'aggiornamento a [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] da un'installazione di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in un'edizione del sistema basata su Itanium di Windows Server 2003 o Windows Server 2003 R2, è necessario prima aggiornare il sistema operativo.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenziali dell'origine dati nell'accesso a URL

 Le stringhe di parametri URL accesso *dsu:datasourcename = value* e *dsp:datasourcename = valore* ora sono obsolete. Nelle versioni precedenti queste stringhe di parametri sono archiviate in testo normale nella cache del browser e non viene pertanto garantita la sicurezza.  
  
## <a name="next-steps"></a>Passaggi successivi

 - [Novità &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [Modifiche del comportamento di SQL Server Reporting Services in SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [Funzionalità deprecate di SQL Server Reporting Services in SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)