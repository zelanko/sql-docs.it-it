---
title: Salvataggio di report (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 01fcf6ef333a9b7c8a5c99630e6e9573f70d8059
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155313"
---
# <a name="saving-reports-report-builder"></a>Salvataggio di report (Generatore report)
  In Generatore report è possibile salvare un report in un server di report, in una raccolta di SharePoint, in una condivisione file su cui si dispone di autorizzazioni di scrittura o nel computer in uso. Il report può essere salvato nello stesso percorso da cui è stato aperto, in un percorso diverso oppure con un nuovo nome nello stesso percorso o in un percorso diverso. Per impostazione predefinita, il salvataggio di un report viene eseguito nuovamente nel percorso da cui è stato aperto il report. Durante il salvataggio di un report, l'elemento che viene effettivamente salvato è la definizione del report che ne descrive il layout. Non vengono salvati i dati. Ogni volta che si esegue il report, i dati del report vengono aggiornati ed è probabile che siano diversi rispetto all'esecuzione precedente del report.  
  
 Se si desidera salvare il report in un formato diverso oppure salvare la definizione del report con i dati, utilizzare una delle seguenti caratteristiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Esportare un report visualizzabile in un formato di file diverso, ad esempio file con valori separati da virgole (CSV) o cartelle di lavoro di Excel, e salvarlo in tale formato. È inoltre possibile generare feed di dati dai report e salvare i dati dei report.  
  
-   Creare sottoscrizioni dei report da recapitare e salvare i report in una condivisione file.  
  
-   Utilizzare la cronologia dei report per salvare versioni di report visualizzabili come copie dei risultati delle esecuzioni dei report in momenti diversi.  
  
 Per altre informazioni sulla visualizzazione e sulla gestione dei report direttamente nel server di report, vedere [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md) e [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md) nella [documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](https://go.microsoft.com/fwlink/?LinkId=154888) nel sito msdn.microsoft.com.  
  
##  <a name="SavingReportDefinitions"></a> Salvataggio delle definizioni dei Report  
 Sebbene sia possibile salvare i report nel computer in uso, il salvataggio in un server di report offre molti vantaggi.  
  
 Il salvataggio di un report in un server di report presenta i vantaggi seguenti:  
  
-   I report vengono resi disponibili per altri utenti che dispongano delle autorizzazioni di accesso alla cartella nella quale è stato salvato il report.  
  
-   I report possono essere gestiti e visualizzati da Gestione report.  
  
-   Le risorse dei report quali le origini dati, le immagini e i sottoreport vengono archiviate in un'unica posizione per un accesso più semplice.  
  
-   I report possono essere recapitati ad altri utenti tramite sottoscrizioni.  
  
-   I report vengono archiviati in modo protetto nel database del server di report.  
  
-   Le esecuzioni dei report possono essere registrate e fornire informazioni sulle prestazioni e sui controlli.  
  
 Il salvataggio di un report in un server di report è noto anche come pubblicazione di un report. Quando si salva il report viene salvata solo la relativa definizione. Ogni volta che si esegue il report, i dati del report vengono aggiornati ed è probabile che siano diversi rispetto all'esecuzione precedente del report. Se si desidera salvare la definizione del report con i dati, è necessario utilizzare la caratteristica di cronologia dei report. Tale caratteristica consente di salvare una copia del report con i relativi dati.  
  

  
##  <a name="ExportingAndSavingReports"></a> Esportazione e salvataggio di report  
 Se il numero di report da archiviare è limitato, è consigliabile esportare un report e salvarlo come file. Dopo aver esportato un report in un'applicazione, ad esempio in formato PDF o Excel, è possibile salvarlo come file e copiarlo in una directory condivisa protetta in rete. In alternativa, è possibile caricare un file PDF o Excel salvato come risorsa se si desidera mantenere tutte le copie del report, indipendentemente dal formato, nel database del server di report. Per altre informazioni sull'esportazione dei report, vedere [esportazione di report &#40;Generatore Report e SSRS&#41; ](export-reports-report-builder-and-ssrs.md) e [carica un File o un Report &#40;gestione Report&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  

  
##  <a name="UsingFileShareDelivery"></a> Utilizzo del recapito tramite condivisione file  
 Se i report da archiviare sono numerosi, è possibile creare una sottoscrizione che recapiti il report direttamente al file system. Per questo approccio è necessario creare una sottoscrizione per ogni report, scegliere una cartella condivisa per archiviare i report e definire una pianificazione che determini quando il file deve essere creato. Quando un utente definisce una sottoscrizione, il server di report è in grado di eseguire automaticamente il report e di aggiungere i file del report all'archivio in base alla pianificazione specificata dall'utente. È inoltre possibile creare pianificazioni a utilizzo singolo per archiviare report occasionalmente. Per ulteriori informazioni sulle sottoscrizioni e sul recapito tramite condivisione file, vedere "Recapito tramite condivisione file in Reporting Services" nella [documentazione di Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di SQL Server.  
  

  
##  <a name="UsingReportHistory"></a> Utilizzo della cronologia dei report  
 È inoltre possibile utilizzare la cronologia dei report per creare copie dei risultati delle esecuzioni dei report in momenti diversi. Per utilizzare queste copie in futuro, è consigliabile eseguire il backup del database del server di report e archiviare tale backup in una posizione sicura. Nel database del server di report viene archiviata l'intera cronologia dei report, insieme ai report, alle origini dei dati condivise, alle cartelle, alle sottoscrizioni e alle pianificazioni condivise. È possibile eseguire il backup per mantenere una copia permanente della cronologia dei report e dei metadati quali le informazioni sulla sottoscrizione che indicano i destinatari di un report. Per ulteriori informazioni, vedere "Gestione della cronologia dei report" nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di SQL Server.  
  

  
##  <a name="HowTo"></a> Procedure  
  
-   [Salvare i report in un server di report &#40;Generatore report&#41;](save-reports-to-a-report-server-report-builder.md)  
  
-   [Salvare un report in una raccolta di SharePoint &#40;Generatore report&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [Salvare i report nel Computer &#40;Generatore Report&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>Vedere anche  
 [Report, parti del report e definizioni dei report &#40;Generatore report e SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Installare, disinstallare e supporto di Generatore Report](../install-uninstall-and-report-builder-support.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportazione di report &#40;Report e SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [Stampa di report &#40;Generatore report e SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
