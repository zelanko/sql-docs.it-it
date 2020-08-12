---
title: Verifica dell'esecuzione di un report | Microsoft Docs
description: Informazioni su come usare i file di log o fare riferimento alle informazioni sullo stato visualizzate con un report per verificare l'esecuzione di un report in Gestione report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6384697eea05d39431ecd7ec77796101747a59ee
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547823"
---
# <a name="verifying-a-report-run"></a>Verifica dell'esecuzione di un report
  Per visualizzare informazioni sullo stato di elaborazione di un report, è possibile utilizzare i file di log oppure controllare le informazioni sullo stato visualizzate con il report in Gestione report.  
  
## <a name="sources-of-report-execution-data"></a>Origini dei dati per l'esecuzione del report  
 I log di esecuzione di un report contengono tutte le informazioni sull'esecuzione del report, tra cui il nome del report, il nome dell'utente che lo ha eseguito, la data e l'ora di esecuzione e l'estensione per il recapito utilizzata per distribuire il report. Per visualizzare e analizzare questi dati, è possibile copiare il log di esecuzione del report in tabelle di database, in modo che sia più semplice eseguire query e creare report sui dati di esecuzione.  
  
 I file di log contengono numerose voci sull'esecuzione dei report e su altre attività del server. Dato che i file di log contengono una così grande quantità di dati, è consigliabile utilizzare Gestione report se si desidera verificare unicamente quando è avvenuta l'ultima esecuzione del report. Se sono necessarie informazioni aggiuntive, è necessario visualizzare i file di log.  
  
> [!NOTE]  
>  In Gestione report non vengono visualizzate la data e l'ora di elaborazione dei report eseguiti su richiesta.  
  
 Nella tabella seguente viene descritto come visualizzare la data e l'ora di elaborazione per vari tipi di report.  
  
|Tipo di report|Posizione delle informazioni sulla data e l'ora|Operazioni da eseguire per visualizzare le informazioni|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Report che viene eseguito come snapshot del report|Pagina Contenuto. Per altre informazioni, vedere [Pagina Contenuto &#40;Gestione report&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378).|1) Individuare la cartella che contiene il report.<br /><br /> 2) Impostare la visualizzazione Dettagli per la cartella.<br /><br /> 3) Osservare data e ora nella colonna **Data ultima esecuzione** .|  
|Snapshot della cronologia del report|Pagina delle proprietà Cronologia. Per altre informazioni, vedere [Pagina delle proprietà Opzioni snapshot &#40;Gestione report&#41;](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).|1) Aprire il report.<br /><br /> 2) Fare clic sulla pagina **Proprietà** .<br /><br /> 3) Fare clic sulla scheda **Cronologia** .<br /><br /> 4) Osservare data e ora nella colonna **Data ultima esecuzione** .|  
|Report memorizzato nella cache|Pianificazione utilizzata per creare e aggiornare il report memorizzato nella cache.|1) Aprire il report.<br /><br /> 2) Fare clic sulla pagina **Proprietà** .<br /><br /> 3) Fare clic sulla scheda **Esecuzione** .<br /><br /> 4) Aprire la pianificazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [File di log e origini di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
