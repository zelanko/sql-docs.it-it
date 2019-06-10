---
title: Salvataggio di report (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8682d55f6c805066f5b596e79a074f253db9faa9
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66499627"
---
# <a name="saving-reports-report-builder"></a>Salvataggio di report (Generatore report)
  In Generatore report è possibile salvare un report impaginato in un server di report di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , in una raccolta di SharePoint, in una condivisione file per la quale si dispone di autorizzazioni di scrittura o nel computer in uso. 
  
Durante il salvataggio di un report, l'elemento che viene effettivamente salvato è la definizione del report che ne descrive il layout. Non vengono salvati i dati. Ogni volta che si esegue il report, i dati del report vengono aggiornati ed è probabile che siano diversi rispetto all'esecuzione precedente del report.  
  
 Se si desidera salvare il report in un formato diverso oppure salvare la definizione del report con i dati, utilizzare una delle seguenti caratteristiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Esportare un report visualizzabile in un formato di file diverso, ad esempio file con valori separati da virgole (CSV) o cartelle di lavoro di Excel, e salvarlo in tale formato. È inoltre possibile generare feed di dati dai report e salvare i dati dei report.  
  
-   Creare sottoscrizioni dei report da recapitare e salvare i report in una condivisione file.  
  
-   Utilizzare la cronologia dei report per salvare versioni di report visualizzabili come copie dei risultati delle esecuzioni dei report in momenti diversi.  
  
 Per altre informazioni sulla visualizzazione e sulla gestione dei report direttamente nel server di report, vedere [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) e [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
##  <a name="SavingReportDefinitions"></a> Salvataggio di report in un server di report  
  Il salvataggio di un report in un server di report è noto anche come pubblicazione di un report. Sebbene sia possibile salvare i report nel computer in uso, il salvataggio in un server di report offre molti vantaggi:  
  
-   I report vengono resi disponibili per altri utenti che dispongano delle autorizzazioni di accesso alla cartella nella quale è stato salvato il report.  
  
-   I report possono essere gestiti e visualizzati nel portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Le risorse dei report quali le origini dati, le immagini e i sottoreport vengono archiviate in un'unica posizione per un accesso più semplice.  
  
-   I report possono essere recapitati ad altri utenti tramite sottoscrizioni.  
  
-   I report vengono archiviati in modo protetto nel database del server di report.  
  
-   Le esecuzioni dei report possono essere registrate e fornire informazioni sulle prestazioni e sui controlli.  
  
##  <a name="ExportingAndSavingReports"></a> Esportazione e salvataggio di report  
 Se il numero di report da archiviare è limitato, è consigliabile esportare un report e salvarlo come file. Dopo aver esportato un report in un'applicazione, ad esempio in formato PDF o Excel, è possibile salvarlo come file e copiarlo in una directory condivisa protetta in rete. In alternativa, è possibile caricare un file PDF o Excel salvato come risorsa se si desidera mantenere tutte le copie del report, indipendentemente dal formato, nel database del server di report. Per altre informazioni sull'esportazione dei report, vedere [Esportare report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) e [Caricare un file o un report](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
##  <a name="UsingFileShareDelivery"></a> Utilizzo del recapito tramite condivisione file  
 Se i report da archiviare sono numerosi, è possibile creare una sottoscrizione che recapiti il report direttamente al file system. Per questo approccio è necessario creare una sottoscrizione per ogni report, scegliere una cartella condivisa per archiviare i report e definire una pianificazione che determini quando il file deve essere creato. Quando un utente definisce una sottoscrizione, il server di report è in grado di eseguire automaticamente il report e di aggiungere i file del report all'archivio in base alla pianificazione specificata dall'utente. È inoltre possibile creare pianificazioni a utilizzo singolo per archiviare report occasionalmente. Per altre informazioni sulle sottoscrizioni e sul recapito tramite condivisione file, vedere [Recapito tramite condivisione file in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
##  <a name="UsingReportHistory"></a> Utilizzo della cronologia dei report  
 È inoltre possibile utilizzare la cronologia dei report per creare copie dei risultati delle esecuzioni dei report in momenti diversi. Per utilizzare queste copie in futuro, è consigliabile eseguire il backup del database del server di report e archiviare tale backup in una posizione sicura. Nel database del server di report viene archiviata l'intera cronologia dei report, insieme ai report, alle origini dei dati condivise, alle cartelle, alle sottoscrizioni e alle pianificazioni condivise. È possibile eseguire il backup per mantenere una copia permanente della cronologia dei report e dei metadati quali le informazioni sulla sottoscrizione che indicano i destinatari di un report. Per altre informazioni, vedere [Creare, modificare ed eliminare snapshot nella cronologia dei report](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
 
##  <a name="HowTo"></a> Procedure  
  
-   [Salvare i report in un server di report &#40;Generatore report&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [Salvare un report in una raccolta di SharePoint &#40;Generatore report&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>Vedere anche  
 [Report, parti del report e definizioni dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Install Report Builder](../install-windows/install-report-builder.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Stampare report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
