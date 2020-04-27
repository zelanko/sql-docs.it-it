---
title: Verifica dell'esecuzione di un report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: c11c57f7c5f67b2557f5637ad10658abc9f80606
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103134"
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
|Report che viene eseguito come snapshot del report|Pagina Contenuto. Per altre informazioni, vedere [Pagina Contenuto &#40;Gestione report&#41;](../contents-page-report-manager.md).|1) Individuare la cartella che contiene il report.<br />2) Impostare la visualizzazione Dettagli per la cartella.<br />3) 3) prendere nota della data e dell'ora della colonna **durante l'esecuzione** .|  
|Snapshot della cronologia del report|Pagina delle proprietà Cronologia. Per altre informazioni, vedere [Pagina delle proprietà Opzioni snapshot &#40;Gestione report&#41;](../snapshot-options-properties-page-report-manager.md).|1) Aprire il report.<br />2) Fare clic sulla pagina **Proprietà** .<br />3) Fare clic sulla scheda **Cronologia** .<br />4) Osservare data e ora nella colonna **Data ultima esecuzione** .|  
|Report memorizzato nella cache|Pianificazione utilizzata per creare e aggiornare il report memorizzato nella cache.|1) Aprire il report.<br />2) Fare clic sulla pagina **Proprietà** .<br />3) Fare clic sulla scheda **Esecuzione** .<br />4) Aprire la pianificazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Impostare proprietà di elaborazione dei report](set-report-processing-properties.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
