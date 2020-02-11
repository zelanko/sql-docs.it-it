---
title: Pianificazione di un report (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c659362e7b5ddba500c2e48df1b11a27a4bf0a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105455"
---
# <a name="planning-a-report-report-builder"></a>Pianificazione di un report (Generatore report)
  Generatore report consente di creare molti tipi di report. Ad esempio è possibile creare report in cui vengono mostrati dati di vendita dettagliati o riepilogativi, tendenze di marketing e di vendite, report operativi o dashboard. È possibile anche creare report con funzionalità avanzate di formattazione del testo, ad esempio per gli ordini di vendita, i cataloghi del prodotto o lettere tipo. Tutti questi report vengono creati utilizzando combinazioni diverse degli stessi blocchi predefiniti di compilazione di Generatore report. Per creare un report utile, facilmente comprensibile, può essere opportuno innanzitutto una pianificazione. Di seguito sono riportate alcune considerazioni da tenere presenti prima di iniziare:  
  
-   **Specificare il formato in cui si desidera visualizzare il report.**  
  
     È possibile eseguire il rendering dei report online in un browser, ad esempio Gestione report, o esportarli in altri formati, ad esempio Excel, Word o PDF. Il formato finale di un report è una scelta importante in quanto non tutte le caratteristiche sono disponibili in tutti i formati di esportazione. Per ulteriori informazioni, vedere [esportazione di report &#40;Generatore report e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
-   **Quale struttura si desidera utilizzare per presentare i dati nel report?**  
  
     Per presentare i dati è possibile scegliere la struttura di tabella, matrice (simile a un report a campi incrociati o di tabella pivot), grafico, formati liberi oppure qualsiasi combinazione di queste strutture. Per ulteriori informazioni, vedere la pagina relativa agli [elenchi &#40;Generatore report e ssrs&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md) e i [grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
-   **Specificare il tipo di report desiderato.**  
  
     Generatore report fornisce molti elementi che possono essere aggiunti al report per semplificarne la lettura, evidenziare le informazioni chiave, facilitarne l'esplorazione da parte dell'utente e così via. La definizione del report consente di determinare se sono necessari elementi del report quali caselle di testo, rettangoli, immagini e righe. Potrebbe inoltre essere necessario mostrare o nascondere elementi, aggiungere una mappa documento, includere report drill-through o sottoreport oppure collegare altri report. Per altre informazioni, vedere [Immagini, caselle di testo, rettangoli e linee &#40;Generatore report e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md) e [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).  
  
-   **Quali dati si desidera visualizzare nei lettori? I dati o il formato devono essere filtrati per destinatari diversi?**  
  
     Potrebbe essere necessario restringere l'ambito del report a utenti o percorsi specifici oppure a un particolare periodo di tempo. Per filtrare i dati del report, utilizzare i parametri per recuperare e visualizzare solo i dati desiderati. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md).  
  
-   **È necessario creare calcoli personalizzati?**  
  
     Talvolta l'origine dati e set di dati non contengono i campi esatti necessari per il report. In tal caso, potrebbe essere necessario creare propri campi calcolati. Ad esempio, potrebbe essere necessario moltiplicare il prezzo per unità per la quantità per ottenere l'importo delle vendite dell'elemento. Sono utilizzate anche le espressioni per fornire la formattazione condizionale e altre caratteristiche avanzate. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
-   **Si desidera nascondere inizialmente gli elementi del report?**  
  
     Potrebbe essere opportuno nascondere gli elementi del report, comprese le aree dati, i gruppi e le colonne, quando il report viene eseguito per la prima volta. Ad esempio, è possibile presentare inizialmente una tabella riepilogativa e successivamente eseguire il drill-down nei dati dettagliati. Per altre informazioni, vedere [Azione di drill-down &#40;Generatore report e SSRS&#41;](drilldown-action-report-builder-and-ssrs.md).  
  
-   **Come si intende recapitare il report?**  
  
     È possibile salvare il report nel computer locale e continuare a utilizzarlo o eseguirlo in locale per informazioni personali. Tuttavia, per condividere il report con altri, è necessario salvarlo in un server di report configurato in modalità nativa o in un server di report in modalità integrata SharePoint. Salvando il report in un server si consente ad altri utenti di poterlo eseguire allorché necessario. In alternativa, l'amministratore del server di report può configurare una sottoscrizione al report o il recapito del report ad altri utenti tramite posta elettronica. È possibile recapitare il report in un formato di esportazione specifico, se desiderato. Per altre informazioni, vedere [Ricerca, visualizzazione e gestione dei report &#40;Generatore report SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore report SQL Server 2014](../report-builder/report-builder-in-sql-server-2016.md)   
 [Concetti relativi alla creazione di report &#40;Generatore report e SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md)  
  
  
