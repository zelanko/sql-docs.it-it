---
title: Aggiungere, spostare o eliminare una tabella, una matrice o un elenco (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3e98a5c49877f6bc94e9e3ac1e880c90229cd3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106594"
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>Aggiunta, spostamento o eliminazione di una tabella, una matrice o un elenco (Generatore report e SSRS)
  In un'area dati vengono visualizzati i dati di un set di dati del report. Le aree dati includono tabelle, matrici, elenchi, grafici e misuratori. Per nidificare un'area dati in un'altra, aggiungere separatamente ogni area dati, quindi trascinare l'area dati figlio nell'area dati padre.  
  
 Per aggiungere un'area dati tabella o matrice al report in modo semplice, eseguire la Creazione guidata tabella o la Creazione guidata matrice. In queste procedure guidate vengono fornite istruzioni utili per scegliere una connessione a un'origine dati, disporre i campi e selezionare il layout e lo stile.  
  
> [!NOTE]  
>  La procedura guidata è disponibile unicamente in Generatore report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>Per aggiungere una tabella o una matrice a un report utilizzando la Creazione guidata tabella o la Creazione guidata matrice  
  
1.  Nella scheda **Inserisci** fare clic su **Tabella** o **Matrice**e quindi scegliere **Creazione guidata tabella** o **Creazione guidata matrice**.  
  
2.  Seguire i passaggi nel **NewTable** oppure **nuova matrice** procedura guidata.  
  
3.  Nella scheda **Home** fare clic su **Esegui** per mostrare il report visualizzabile.  
  
4.  Nella scheda **Esegui** fare clic su **Progettazione** per continuare a utilizzare il report.  
  
### <a name="to-add-a-data-region"></a>Per aggiungere un'area dati  
  
1.  Nel gruppo **Aree dati**sulla **barra multifunzione** fare clic sull'area dati da aggiungere.  
  
2.  Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella delle dimensioni desiderate per l'area dati.  
  
3.  Trascinare un campo del set di dati del report dal riquadro dei dati del report in una cella dell'area dati. L'area dati risulterà associata ai dati del set di dati del report.  
  
### <a name="to-select-a-data-region"></a>Per selezionare un'area dati  
  
-   Per un'area dati Tablix, fare clic con il pulsante destro del mouse sull'handle d'angolo. Per un'area dati grafico o misuratore, fare clic nell'area dati.  
  
     Verranno visualizzati un handle di selezione e otto handle di ridimensionamento.  
  
     Per le aree dati annidate, fare clic con il pulsante destro del mouse nell'area dati annidata, scegliere **Seleziona**e quindi selezionare l'elemento del report desiderato. Per verificare quale elemento del report è selezionato, utilizzare il riquadro Proprietà. Il nome dell'elemento selezionato nell'area di progettazione verrà visualizzato sulla barra degli strumenti del riquadro Proprietà.  
  
### <a name="to-move-a-data-region"></a>Per spostare un'area dati  
  
-   Per spostare un'area dati, fare clic sull'handle di selezione dell'area dati e trascinarlo. Utilizzare guide di allineamento per allineare l'area dati agli elementi di report esistenti.  
  
     Se il righello non è visibile, fare clic sulla scheda Visualizza e selezionare l'opzione **Righello** .  
  
     In alternativa, utilizzare i tasti di direzione per spostare l'area dati selezionata nell'area di progettazione.  
  
### <a name="to-delete-a-data-region"></a>Per eliminare un'area dati  
  
-   Selezionare l'area dati, fare clic con il pulsante destro del mouse nell'area dati e quindi scegliere **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
