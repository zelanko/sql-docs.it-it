---
title: Cosa&#39;s novità di Generatore Report per SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8223c19b-4b0d-4b1d-a042-9a726c18e708
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: b3b79652df1ae0265e281f78626c0f880b21866c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027862"
---
# <a name="what39s-new-in-report-builder-for-sql-server-2014"></a>Cosa&#39;s novità di Generatore Report per SQL Server 2014
  In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] sono state introdotte numerose funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Per informazioni sulle funzionalità disponibili in questa versione per altri [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] prodotti e tecnologie, vedere [What ' s New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
> [!TIP]  
>  Per informazioni più recenti e le risorse relative alle nuove funzionalità in questa versione, vedere [informazioni aggiuntive sulle novità in SQL Server Reporting Services (SSRS)](https://go.microsoft.com/fwlink/?LinkId=207147).  
  
##  <a name="ExcelRenderer"></a> Renderer di Excel per Microsoft Excel 2007-2010 e Microsoft Excel 2003  
 L'estensione per il rendering di Excel in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], nuova in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], consente di eseguire il rendering di un report come documento di Excel compatibile con [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2007-2010 e con [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2003 grazie a Microsoft Office Compatibility Pack per i formati di file Word, Excel e PowerPoint. Il formato è Office Open XML mentre l'estensione di file è xlsx.  
  
 Con questa estensione per il rendering di Excel vengono rimosse le limitazioni della versione precedente, compatibile con Excel 2003. Di seguito sono elencati i miglioramenti dell'estensione per il rendering:  
  
-   Il numero massimo di righe per foglio di lavoro è 1.048.576.  
  
-   Il numero massimo di colonne per foglio di lavoro è 16.384.  
  
-   Il numero di colori consentiti in un foglio di lavoro è di circa 16 milioni (colore a 24 bit).  
  
-   La compressione ZIP consente una riduzione delle dimensioni dei file.  
  
 Per altre informazioni, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
##  <a name="WordRenderer"></a> Renderer di Word per Microsoft Word 2007-2010 e Microsoft Word 2003  
 L'estensione per il rendering di Word in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], nuova in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], consente di eseguire il rendering di un report come documento di Word compatibile con [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2007-2010 e con [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2003 grazie a [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Compatibility Pack per i formati di file Word, Excel e PowerPoint. Il formato è Office Open XML mentre l'estensione di file è docx.  
  
 Oltre a rendere le funzionalità che sono nuove in Word 2007-2010 disponibili per i report esportati, i file *.docx di report esportati tendono a essere più piccoli. I report esportati tramite il renderer di Word sono in genere notevolmente più piccoli rispetto agli stessi report esportati utilizzando il renderer di Word 2003.  
  
 Per altre informazioni, vedere [Esportazione in Microsoft Word &#40;Generatore report e SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
