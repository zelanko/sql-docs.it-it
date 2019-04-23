---
title: 'Lezione 3: Progettare il Report padre tramite la creazione guidata rapporto | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8fe60270cd3737e3c372fbf92ccb906beb8d06cb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940236"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>Lezione 3: Progettare il report padre tramite la Creazione guidata report
  Dopo aver creato una connessione dati e una tabella di dati per il report padre, il passaggio successivo consiste nel progettare il report padre utilizzando la Creazione guidata report in Progettazione report. Per altre informazioni sulla progettazione dei report, vedere [Progettare report con Progettazione report &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>Per progettare il report padre tramite la Creazione guidata report  
  
1.  Verificare che in **Esplora soluzioni**sia selezionato il sito Web principale.  
  
2.  Fare clic con il pulsante destro del mouse sul sito Web e selezionare **Add New Item**(Aggiungi nuovo elemento).  
  
3.  Nel **Aggiungi nuovo elemento** finestra di dialogo **Creazione guidata rapporto**, immettere un nome per il file di report e quindi fare clic su **Add**.  
  
     Verrà avviata la Creazione guidata report.  
  
4.  Nel **proprietà set di dati** nella pagina il **zdroj dat** , quindi selezionare il **DataSet1** creato in [lezione 2: Definire una connessione dati e un tabella di dati per il Report padre](lesson-2-define-a-data-connection-and-data-table-for-parent-report.md).  
    La casella **Available datasets** (Set di dati disponibili) viene aggiornata automaticamente con l'oggetto **DataTable** creato in precedenza.  
  
5.  Scegliere **Avanti**.  
  
6.  Nella pagina **Disponi campi** eseguire le operazioni seguenti:  
  
    1.  Trascinare **ProductID**, **Name**, **ProductNumber**, **SafetyStockLevel**, e **ReorderLevel** da **Campi disponibili** alla casella **Valori** .  
  
    2.  Fare clic sulla freccia accanto a **SUM (ProductID)**, **SUM (safetystocklevel)**, **SUM (ReorderLevel)** e deselezionare il **somma** selezione.  
  
7.  Fare clic su **successivo** due volte, quindi fare clic su **Finish** per chiudere la **Creazione guidata Report**.  
  
     È stato creato il file con estensione rdlc. Il file viene aperto in Progettazione report. La Tablix che è stata progettata è ora visualizzata nell'area di progettazione.  
  
8.  Salvare il file con estensione rdlc.  
  
## <a name="next-task"></a>Attività successiva  
 È stato progettato correttamente il report padre tramite la Creazione guidata report. Successivamente, verranno create una connessione dati e una tabella di dati per il report figlio.  
  
  
