---
title: 'Attività 10: aggiunta della trasformazione Raggruppamento fuzzy per identificare i duplicati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e7091c4dbb8244476357afba18e973535def8baa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064807"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>Attività 10: Aggiunta della trasformazione Raggruppamento fuzzy per l'identificazione di duplicati
  In questa attività viene aggiunta una trasformazione Raggruppamento fuzzy al flusso di dati. La trasformazione Raggruppamento fuzzy consente di identificare i duplicati nei dati di origine. Per altri dettagli, vedere [trasformazione Raggruppamento fuzzy](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) .  
  
1.  Trascinare la trasformazione **Raggruppamento fuzzy** in **altre trasformazioni** nella **casella degli strumenti SSIS** nella scheda **flusso di dati** in **Combina record corretti e con correzione**.  
  
2.  Fare clic con il pulsante destro del mouse su trasformazione **Raggruppamento fuzzy** nella scheda **flusso di dati** e scegliere **Rinomina**. Digitare **Group Suppliers con ID corrispondenti** e premere **invio**.  
  
3.  Connetti **Combina record corretti e con correzione** per **raggruppare i fornitori con ID corrispondenti** usando il connettore blu.  
  
     ![Connessione a Raggruppa fornitori con ID corrispondenti](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Connessione a Raggruppa fornitori con ID corrispondenti")  
  
4.  Fare doppio clic su **Raggruppa fornitori con ID corrispondenti**.  
  
5.  **Nell'Editor trasformazione Raggruppamento fuzzy**fare clic su **nuovo** accanto all'elenco a **discesa Gestione connessione OLE DB** per avviare la finestra di dialogo **Configura OLE DB gestione connessione** .  
  
6.  Nella finestra di dialogo fare clic su **nuova** per avviare la finestra di dialogo **gestione connessione** .  
  
7.  Digitare **(local)** o **period** (.) per il nome del server.  
  
8.  Selezionare **MDS** per **selezionare un campo o immettere un nome di database** . Il database MDS sarà utilizzato come archivio temporaneo per la **trasformazione Raggruppamento fuzzy**. La trasformazione **Raggruppamento fuzzy** richiede una connessione a un'istanza di SQL Server creare le tabelle SQL Server temporanee necessarie all'algoritmo di trasformazione per eseguire il lavoro. A tal fine, è possibile creare un database o utilizzarne un altro esistente.  
  
9. Fare clic su **Test connessione** per testare la connessione e fare clic su **OK** nella finestra di messaggio.  
  
10. Nella finestra di dialogo **gestione connessione** fare clic su **OK**.  
  
11. Selezionare **(locale). MDS** (o **localhost). MDS**) nell' **elenco di connessioni dati** e fare clic su **OK**.  
  
12. In **Editor trasformazione Raggruppamento fuzzy**confermare che **(locale). MDS** o **localhost. MDS** è selezionato per la **gestione connessione OLE DB**.  
  
13. Passare alla scheda **colonne** .  
  
14. Selezionare (casella di controllo) **SupplierID_Output** dall'elenco delle **colonne di input disponibili**. Per configurare la trasformazione, selezionare le colonne di input da utilizzare per l'identificazione dei duplicati. Per mantenerla semplice, utilizzare solo SupplierID in questo passaggio.  
  
     ![Editor trasformazione Raggruppamento fuzzy](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "Editor trasformazione Raggruppamento fuzzy")  
  
15. Fare clic su **OK** per chiudere l' **Editor trasformazione Raggruppamento fuzzy**.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 11: Aggiunta della trasformazione Suddivisione condizionale a Filtra duplicati](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
