---
title: Report, parti del report e definizioni dei report (Generatore report) | Microsoft Docs
description: Informazioni sui termini usati per descrivere i report in stati diversi in Generatore report. Questi stati includono la definizione iniziale e il report pubblicato.
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 53e8c7fcd6765742af0056fb44659386cf652561
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039720"
---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>Report, parti del report e definizioni dei report (Generatore report e SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa vari termini per descrivere un report impaginato nei diversi stati, inclusi la definizione iniziale, il report pubblicato e il report così come viene visualizzato dall'utente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>File di definizione del report (con estensione rdl)  
 Una definizione del report è un file che viene creato dall'utente in Generatore report o Progettazione report. Tale file fornisce una descrizione completa delle connessioni alle origini dati, delle query utilizzate per il recupero dei dati, delle espressioni, dei parametri, delle immagini, delle caselle di testo, delle tabelle e di qualsiasi altro elemento relativo alla fase di progettazione che si desidera includere in un report. Sebbene le definizioni del report possano essere complesse, nella versione più semplice specificano una query e altro contenuto per il report, nonché le proprietà e il layout del report.  
  
 Le definizioni del report vengono visualizzate in fase di esecuzione come report elaborato. Durante questa fase, i dati vengono recuperati dall'origine dati e formattati in base alle istruzioni contenute nella definizione del report. Una definizione del report può essere eseguita direttamente dal computer e salvata in locale o può essere pubblicata su un server di report per consentire ad altri utenti di eseguirla.  
  
 Le definizioni del report vengono scritte in codice XML in conformità a una grammatica XML denominata linguaggio RDL (Report Definition Language). Il linguaggio RDL descrive gli elementi XML che definiscono tutte le possibili varianti di un report.  
  
## <a name="client-report-definition-rdlc-files"></a>File di definizione del report del client (con estensione rdlc)  
 In Progettazione report di Visual Studio vengono creati file di definizione del report del client (con estensione rdlc) da utilizzare con il controllo ReportViewer. Tali file possono essere convertiti in file con estensione rdl da utilizzare con Progettazione report di Reporting Services.  
  
## <a name="report-part-rsc-files"></a>File della parte del report (con estensione rsc)  
 Le parti del report sono elementi autonomi del report archiviati sul server di report e possono essere incluse in altri report. Usare Generatore report per cercare e selezionare parti della Raccolta parti del report da aggiungere ai report. Usare Progettazione report o Generatore report per salvare parti del report da usare nella Raccolta parti del report.  
  
 Una definizione di parte del report è un frammento XML di un file di definizione del report. Le parti del report vengono create da una definizione del report e dalla successiva selezione degli elementi nel report da pubblicare separatamente come parti del report. Nelle parti del report sono incluse aree dati, rettangoli e relativi elementi contenuti nonché immagini. È possibile salvare una parte del report con i relativi set di dati dipendenti e i riferimenti alle origini dati condivise in modo da poterla riutilizzare negli altri report.  
  
 Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) e [Parti del report in Progettazione report &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
## <a name="published-reports"></a>Report pubblicati  
 Dopo aver creato un file con estensione rdl, è possibile salvarlo in locale o in una cartella personale, ad esempio la cartella Report personali, sul server di report. Quando il report è pronto per la visualizzazione da parte di altri utenti, è possibile pubblicarlo salvandolo da Generatore report in una cartella pubblica nel server di report, caricandolo tramite il portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o distribuendo una soluzione di progetto report da Progettazione report. Un report pubblicato è un elemento archiviato in un database del server di report e gestito su un server di report o in un sito di SharePoint.  
  
 Un report pubblicato viene protetto mediante l'assegnazioni di ruolo utilizzando il modello di sicurezza basata sui ruoli di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . L'accesso ai report pubblicati viene eseguito tramite URL, web part di SharePoint o il portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . In alternativa, è possibile passare ai report pubblicati e aprirli in Generatore report.  
  
### <a name="report-snapshots"></a>Snapshot del report  
 I report possono essere pubblicati anche sotto forma di snapshot che contiene sia informazioni sul layout che dati, ad esempio l'ora di inizio di esecuzione del report. Gli snapshot dei report non vengono salvati in un formato di rendering specifico, ma ne viene eseguito il rendering nel formato di visualizzazione finale, ad esempio HTML, solo quando vengono richiesti da un utente o un'applicazione. Per altre informazioni, vedere [Ricerca e visualizzazione di report nel portale Web](../report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md).  
  
## <a name="rendered-reports"></a>Report visualizzabili  
 Un report visualizzabile è un report completamente elaborato che include i dati e le informazioni sul layout in un formato appropriato per la visualizzazione, ad esempio HTML. Non è possibile visualizzare un report fino a quando non ne viene eseguito il rendering in un formato di output. È possibile eseguire il rendering di un report eseguendo una delle operazioni seguenti:  
  
-   Creare o aprire un report in Generatore report o Progettazione report ed eseguirlo.  
  
-   Trovare ed eseguire un report nel portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Trovare ed eseguire un report in un sito di SharePoint integrato con un server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Sottoscrivere un report, che viene recapitato a una cartella Posta in arrivo o a una condivisione file in un formato di output specificato dall'utente.  
  
 Sottoscrivere un report, che viene recapitato a una cartella Posta in arrivo o a una condivisione file in un formato di output specificato dall'utente. Il formato di rendering predefinito per un report è HTML 4.0. Oltre al formato HTML, sono disponibili vari formati di output in cui è possibile eseguire il rendering dei report, inclusi i formati Excel, Word, XML, PDF, TIFF e CSV. Come per i report pubblicati, anche i report visualizzabili non possono essere modificati o salvati nuovamente su un server di report. Per altre informazioni, vedere [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi a Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md)[Generatore report in SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
