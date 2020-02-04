---
title: Creare un report per dispositivi mobili di Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3fd0fc3530ec35da61e2314ef7a80a58d9bdd7d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63316427"
---
# <a name="create-a-reporting-services-mobile-report"></a>Creare un report per dispositivi mobili di Reporting Services
Con SQL Server Mobile Report Publisher è possibile creare rapidamente report per dispositivi mobili di SQL Server Reporting Services che si adattano alle dimensioni di qualsiasi schermo, in un'area di progettazione con righe e colonne della griglia di dimensioni variabili ed elementi flessibili dei report per dispositivi mobili.  
  
La prima volta che si crea un report per dispositivi mobili è possibile installare SQL Server Mobile Report Publisher nel computer locale dal portale Web di Reporting Services. In alternativa, è possibile installarlo dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=733527). Successivamente, è possibile avviarlo dal portale Web o in locale.   
    
1. Nella barra superiore del portale Web di Reporting Services selezionare **Nuovo** > **Report per dispositivi mobili**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Nella scheda **Layout** di Mobile Report Publisher selezionare uno strumento di navigazione, un misuratore, un grafico, una mappa o una griglia dati e trascinare l'elemento nella griglia di struttura.  
  
3. Fare clic sull'angolo inferiore destro dell'elemento e trascinarlo fino a ottenere le dimensioni desiderate.  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   Questa è la griglia di progettazione **Master** in cui creare gli elementi da includere nel report. Successivamente, è possibile [definire il layout del report per un tablet o un telefono](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md).     
     
   In **Proprietà visive** sotto la griglia di progettazione notare le diverse proprietà che è possibile impostare.  
     
4. Selezionare la scheda **Dati** nell'angolo in alto a sinistra e notare che al grafico sono già associati dati simulati.   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. Selezionare **Aggiungi dati** nell'angolo in alto a destra.  
  
6. Selezionare **Excel locale** o **Server di report**.  
  
   >**Suggerimenti**: se si intende aggiungere dati da Excel, assicurarsi che:  
    >* [I dati di Excel siano preparati](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) per l'uso nel report per dispositivi mobili.  
    >* Chiudere prima il file.  
7. Selezionare i fogli di lavoro desiderati e scegliere **Importa**.   
   È possibile aggiungere contemporaneamente più fogli di lavoro di una cartella di lavoro.  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. Sempre nella scheda **Dati** , nella casella **Proprietà dati** selezionare la tabella e i campi da includere nel grafico.  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. Tornare alla scheda **Layout** . Nella casella **Proprietà visive** è possibile impostare proprietà quali **Titolo**, **Unità di tempo**e **Formato numeri**.  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. Selezionare **Anteprima** in alto a sinistra per visualizzare l'aspetto del report.  
  
11. A questo punto è necessario salvare il report. Selezionare l'icona Salva nell'angolo in alto a sinistra e quindi **Salva in locale** o **Salva nel server**.  
  
   Per il salvataggio in un server è necessario accedere a un server di report di SQL Server Reporting Services.  
     
   ### <a name="see-also"></a>Vedere anche  
     
-   [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [Layout di un report Reporting Services per dispositivi mobili per telefono o tablet](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   
