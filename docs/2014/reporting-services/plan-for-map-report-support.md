---
title: Piano di supporto dei Report mappa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df796e2dd4e132164f00716a9cb12f7b498d8984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108075"
---
# <a name="plan-for-map-report-support"></a>Pianificare il supporto dei report mappa
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] supporta i report di mappa che utilizzano origini dati spaziali. I dati spaziali possono provenire da database di SQL Server, da file di forma ESRI o dalla raccolta mappe installata con Reporting Services o Generatore report. In una mappa è inoltre possibile visualizzare uno sfondo a sezioni di Bing Map. L'autore del report è possibile creare un report che specifica i dati spaziali o sezioni di Bing map come dinamici e recuperati in fase di esecuzione o come statici e incorporati nella definizione del report.  
  
## <a name="support-for-bing-maps"></a>Supporto per Bing Maps  
 Le mappe possono includere un livello sfondo che consente di visualizzare sezioni di Bing Map. Per visualizzare un report pubblicato che dispone di un livello sezione mappa, è necessario configurare il server di report per recuperare sezioni dai servizi Web di Bing Maps. Per altre informazioni, vedere [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md).  
  
 In ogni report gli autori del report possono specificare se utilizzare una connessione Secure Sockets Layer (SSL) per recuperare sezioni dal server delle sezioni. A tale scopo, nel riquadro proprietà per il livello sezione, è necessario impostare la proprietà booleana UseSecureConnection a `true`.  
  
> [!NOTE]  
>  Per altre informazioni sull'utilizzo delle tessere mappa di Bing nel report, vedere [Ulteriori condizioni di utilizzo](https://go.microsoft.com/fwlink/?LinkId=151371) e [Informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkId=151372).  
  
## <a name="report-design-recommendations"></a>Indicazioni sulla progettazione di report  
 Una buona progettazione di report per i report delle mappe richiede una valutazione da parte dell'autore in termini di compromessi tra i dati spaziali statici e quelli dinamici nonché l'individuazione di un equilibrio utile agli utenti dei report. Gli elementi della mappa incorporati possono aumentare notevolmente le dimensioni della definizione del report, ma riducono il tempo necessario per visualizzare il report della mappa. Gli elementi dinamici della mappa riducono le dimensioni della definizione del report, ma aumentano il tempo necessario per elaborare e visualizzare la mappa. L'autore del report deve trovare il giusto equilibrio tra questi due aspetti.  
  
 Quando le dimensioni della definizione del report rappresentano un problema, in qualità di amministratore del server di report, è possibile incoraggiare i progettisti di report a ridurre la quantità di dati spaziali in una definizione del report.  
  
 Nelle condizioni seguenti, gli elementi della mappa vengono incorporati nella definizione del report:  
  
-   Quando viene creato il report, l'origine dati spaziali si trova sul file system locale. Sono inclusi i dati spaziali della raccolta mappe o i file di forma ESRI installati localmente. Per impostazione predefinita, la Creazione guidata mappa e la Creazione guidata livello mappa incorporano dati spaziali dalle origini dati nel file system locale.  
  
-   L'autore del report sceglie l'opzione per incorporare manualmente i dati spaziali nel report.  
  
 Per ridurre le dimensioni delle definizioni dei report che dispongono di mappe, gli autori del report possono utilizzare una o più delle opzioni seguenti:  
  
-   Da Progettazione report in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], aggiungere origini dati spaziali, ovvero file di forma ESRI, al progetto server di report. Quando il progetto viene distribuito, i file di forma ESRI vengono pubblicati nel server di report in aggiunta al report. Quando l'autore del report esegue la Creazione guidata mappa, è possibile specificare un'origine dati spaziali dal progetto server di report e, per impostazione predefinita, gli elementi della mappa non sono incorporati nelle definizioni del report.  
  
-   Da Generatore report, aggiungere origini dati spaziali che sono file di forma ESRI selezionando i file di forma dal server di report. Quando l'autore del report esegue la Creazione guidata mappa, è possibile sfogliare e selezionare un'origine dati spaziali dal server di report e, per impostazione predefinita, gli elementi della mappa non sono incorporati nelle definizioni del report.  
  
-   Quando i dati mappa devono essere incorporati, regolare il centro del viewport e il livello di zoom per includere solo i dati mappa necessari per il report.  
  
 Per altre informazioni, [Maps &#40;Generatore Report e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Risolvere problemi relativi ai report: Report mappa &#40;Generatore report e SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
