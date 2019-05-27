---
title: "Lezione 6: Aggiungere un controllo ReportViewer all'applicazione | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfce5e2bdf71dfb58481fedf05794d3603285449
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108414"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>Lezione 6: Aggiungere un controllo ReportViewer all'applicazione
  Dopo aver progettato il report figlio tramite la Creazione guidata report, il passaggio successivo consiste nell'aggiungere un controllo ReportViewer all'applicazione del sito Web.  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>Per aggiungere un controllo ReportViewer all'applicazione  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Default.aspx**, quindi scegliere **Progettazione viste**.  
  
2.  Dal gruppo **Estensioni AJAX** nella finestra della **casella degli strumenti** trascinare un controllo **ScriptManager** nell'area di progettazione.  
  
3.  Dal gruppo **Report** trascinare un controllo **ReportViewer** nell'area di progettazione sotto il controllo **ScriptManager** .  
  
4.  Aprire la finestra **Attività di ReportViewer** facendo clic sulla freccia nell'angolo superiore destro del controllo **ReportViewer** .  
  
5.  Nella casella **Scegli report** selezionare il report padre creato.  
  
     Quando si seleziona un report, le istanze delle origini dati utilizzate nel report vengono create automaticamente. Il codice viene generato per la creazione di un'istanza di ogni oggetto DataTable e del relativo contenitore [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) . Un controllo [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) viene aggiunto all'area di progettazione, corrispondente a ogni origine dati usata nel report. Questo controllo dell'origine dati viene configurato automaticamente.  
  
     Se si usa Microsoft Visual Studio 2012, assicurarsi che il controllo ObjectDataSource sia associato a DataSet1, completo con lo spazio dei nomi di progetto, se il nome completo è elencato nel **Seleziona oggetto business**casella di riepilogo a discesa (ad esempio Projectnamespace.DataSet1TableAdapters.ProductTableAdapter). Accedere alla casella di riepilogo facendo clic con il pulsante destro del mouse su ObjectDataSource e scegliendo **Configura origine dati**.  
  
6.  Scegliere Compila sito Web dal menu Compila.  
  
     Il report viene compilato e tutti gli errori, ad esempio un errore di sintassi in un'espressione del report, vengono visualizzati nell'area **Elenco errori** . Fare clic su **Elenco errori** nella parte inferiore della finestra di Visual Studio per visualizzare l'area **Elenco errori** .  
  
## <a name="next-task"></a>Attività successiva  
 È stato aggiunto correttamente un controllo ReportViewer all'applicazione del sito Web. Successivamente, si aggiungerà un'azione drill-through nel report padre.  
  
  
