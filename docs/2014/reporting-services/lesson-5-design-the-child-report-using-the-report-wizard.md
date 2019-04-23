---
title: 'Lezione 5: Progettare il Report figlio tramite la creazione guidata rapporto | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd86b5b8b6466f6075f2b3c8814fb13a8ec62d9a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959927"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lezione 5: Progettare il report figlio tramite la Creazione guidata report
  Dopo aver creato una connessione dati e una tabella di dati per il report figlio, il passaggio successivo consiste nel progettare il report figlio utilizzando la Creazione guidata report in Progettazione report. Per altre informazioni sulla progettazione dei report, vedere [Progettare report con Progettazione report &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Per progettare il report figlio tramite la Creazione guidata report  
  
1.  Verificare che in **Esplora soluzioni**sia selezionato il sito Web principale.  
  
2.  Fare clic con il pulsante destro del mouse sul sito Web e selezionare **Add New Item**(Aggiungi nuovo elemento).  
  
3.  Nel **Aggiungi nuovo elemento** finestra di dialogo, fare clic su **Creazione guidata rapporto**, immettere un nome per il file di report e quindi fare clic su **Add**.  
  
     Verrà avviata la Creazione guidata report.  
  
4.  Nel **proprietà set di dati** pagina il **zdroj dat** fare clic su **DataSet2**.  
  
     La casella **Available datasets** (Set di dati disponibili) viene aggiornata automaticamente con l'oggetto DataTable che è stato creato.  
  
5.  Scegliere **Avanti**.  
  
6.  Nella pagina **Disponi campi** eseguire le operazioni seguenti:  
  
    1.  Trascinare **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**e **StockedQty** da **Campi disponibili** nella casella **Valori** .  
  
    2.  Fare clic sulla freccia accanto a **SUM (ProductID)**, **SUM (purchaseorderid)**, **SUM (purchaseorderdetailid)**, **SUM (OrderQty)**,  **SUM (receivedqty)**, **SUM (rejectedqty)**, e **SUM (stockedqty)** e deselezionare il **somma** selezione.  
  
7.  Fare clic su **successivo** due volte, quindi fare clic su **Finish** per chiudere la **Creazione guidata Report**.  
  
     È stato creato il file con estensione rdlc. Il file viene aperto in Progettazione report. La Tablix che è stata progettata è ora visualizzata nell'area di progettazione.  
  
8.  Con il file con estensione rdlc aperto, aggiungere un parametro effettuando le operazioni seguenti:  
  
    1.  Fare clic su **parametri** nel **i dati del Report** riquadro e quindi fare clic su **aggiunta parametri**.  
  
    2.  Immettere **productid** nella casella **Nome** .  
  
    3.  Verificare che sia selezionato **Integer** nella casella di riepilogo **Data Type** .  
  
    4.  Fare clic su **OK**.  
  
9. Salvare il file con estensione rdlc.  
  
## <a name="next-task"></a>Attività successiva  
 È stato progettato correttamente il report figlio tramite la Creazione guidata report. Successivamente, si aggiungerà un controllo ReportViewer all'applicazione del sito Web.  
  
  
