---
title: 'Lesson 5: Design the Child Report using the Report Wizard (Lezione 5: Progettare il report figlio tramite la Creazione guidata report) | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: da9f07cf60a2ec42e23416b52cbfebab78802247
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512645"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lezione 5: Progettare il report figlio tramite la Creazione guidata report
Dopo aver creato una connessione dati e una tabella di dati per il report figlio, il passaggio successivo consiste nel progettare il report figlio utilizzando la Creazione guidata report in Progettazione report. Per altre informazioni sulla progettazione dei report, vedere [Progettare report con Progettazione report &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Per progettare il report figlio tramite la Creazione guidata report  
  
1.  Verificare che in **Esplora soluzioni**sia selezionato il sito Web principale.  
  
2.  Fare clic con il pulsante destro del mouse sul sito Web e selezionare **Add New Item**(Aggiungi nuovo elemento).  
  
3.  Nella finestra di dialogo **Add New Item** (Aggiungi nuovo elemento) fare clic su **Creazione guidata report**, immettere un nome per il file di report e scegliere **Aggiungi**.  
  
    Verrà avviata la Creazione guidata report.  
  
4.  Nella casella **Origine dati** della pagina **Proprietà set di dati** fare clic su **DataSet2**.  
  
    La casella **Available datasets** (Set di dati disponibili) viene aggiornata automaticamente con l'oggetto DataTable che è stato creato.  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **Disponi campi** eseguire le operazioni seguenti:  
  
    1.  Trascinare **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**e **StockedQty** da **Campi disponibili** nella casella **Valori** .  
  
    2.  Fare clic sulla freccia accanto a **Sum(ProductID)** , **Sum(PurchaseOrderID)** , **Sum(PurchaseOrderDetailID)** , **Sum(OrderQty)** , **Sum(ReceivedQty)** , **Sum(RejectedQty)** e **Sum(StockedQty)** e deselezionare **Sum** .  
  
7.  Fare clic due volte su **Avanti** e selezionare **Fine** per chiudere la **Creazione guidata report**.  
  
    È stato creato il file con estensione rdlc. Il file viene aperto in Progettazione report. La Tablix che è stata progettata è ora visualizzata nell'area di progettazione.  
  
8.  Con il file con estensione rdlc aperto, aggiungere un parametro effettuando le operazioni seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse su **Parametri** nel riquadro **Dati report** e scegliere **Aggiunta parametri**.  
  
    2.  Immettere **productid** nella casella **Nome** .  
  
    3.  Verificare che sia selezionato **Integer** nella casella di riepilogo **Data Type** .  
  
    4.  Fare clic su **OK**.  
  
9. Salvare il file con estensione rdlc.  
  
## <a name="next-task"></a>Attività successiva  
È stato progettato correttamente il report figlio tramite la Creazione guidata report. Successivamente, si aggiungerà un controllo ReportViewer all'applicazione del sito Web. Vedere [Lezione 6: Aggiungere un controllo ReportViewer all'applicazione](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md).  
  
  
  

