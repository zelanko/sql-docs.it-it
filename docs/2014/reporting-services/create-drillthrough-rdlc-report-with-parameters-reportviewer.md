---
title: Creare un report drill-through (RDLC) con parametri usando ReportViewer (esercitazione su SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7efb713b5dbf9a3f19118bb3572ccd35778aad19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109644"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>Creare un report drill-through (RDLC) con parametri utilizzando ReportViewer (esercitazione su SSRS)
  Un report [drill-through](https://technet.microsoft.com/library/ff519554.aspx) è un report aperto da un utente facendo clic su un collegamento in un altro report. Nei report drill-through sono solitamente disponibili dettagli relativi a un elemento contenuto in un report di riepilogo originale. In questa esercitazione verranno illustrate le seguenti lezioni sulla creazione di un report drill-through con parametri e una query, in [report in modalità locale](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
## <a name="requirements"></a>Requisiti  
 Per utilizzare questa procedura dettagliata, è necessario poter accedere al database di esempio **AdventureWorks2008** . La query utilizzata in questa procedura dettagliata verrà utilizzata anche per il database **AdventureWorks2012** . Per altre informazioni su come ottenere il database di esempio **AdventureWorks2008** , vedere [Procedura dettagliata: installazione del database AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) per Microsoft Visual Studio 2010.  
  
 Questa procedura dettagliata presuppone che l'utente abbia familiarità con le query Transaction-SQL e gli oggetti [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) e [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) di ADO.NET.  
  
 Utilizzare Visual Studio 2010 o Visual Studio 2012 e il modello di sito Web ASP.NET per creare una pagina Web ASP.NET con un controllo ReportViewer. Il controllo è configurato per visualizzare un report che viene creato. Per questa procedura dettagliata viene creata l'applicazione in Microsoft Visual C#.  
  
## <a name="tasks"></a>Attività  
 [Lezione 1: creare un nuovo sito Web](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [Lezione 2: definire una connessione dati e una tabella di dati per il report padre](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [Lezione 3: progettare il report padre utilizzando la creazione guidata report](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [Lezione 4: definire una connessione dati e una tabella di dati per il report figlio](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [Lezione 5: progettare il report figlio utilizzando la creazione guidata report](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [Lezione 6: aggiungere un controllo ReportViewer all'applicazione](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [Lezione 7: aggiungere un'azione drill-through nel report padre](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [Lezione 8: creare un filtro di dati](../reporting-services/lesson-8-create-a-data-filter.md)   
 [Lezione 9: Compilare ed eseguire l'applicazione](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Progettare report con Progettazione report &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
