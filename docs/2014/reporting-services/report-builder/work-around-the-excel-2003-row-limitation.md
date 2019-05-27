---
title: Soluzione alternativa alla limitazione di righe di Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f01e85a0a93ef1f2a14b2b01b4180143153865
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107544"
---
# <a name="work-around-the-excel-row-limitation"></a>Soluzione alternativa per il limite di righe in Excel
  In questo argomento viene illustrato come risolvere il limite di righe di Excel 2003 quando si esportano i report in Excel. La soluzione alternativa consiste in un report contenente una sola tabella.  
  
 Excel 2003 supporta un massimo di 65.536 righe per foglio di lavoro. È possibile risolvere questo limite forzando un'interruzione di pagina esplicita dopo un determinato numero di righe. Tramite il renderer Excel viene creato un nuovo foglio di lavoro per ogni interruzione di pagina esplicita.  
  
### <a name="to-create-an-explicit-page-break"></a>Per creare un'interruzione di pagina esplicita  
  
1.  Aprire il report in [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] o Gestione report.  
  
2.  Fare clic con il pulsante destro del mouse sulla riga dei dati nella tabella, quindi scegliere **Aggiungi gruppo** > **Gruppo padre** per aggiungere un gruppo di tabelle esterno.  
  
     ![Selezionare Gruppo padre](../media/datarow-selectparentgroup.png "Selezionare Gruppo padre")  
  
3.  Immettere la formula seguente nella casella dell'espressione **Raggruppa per** , quindi fare clic su **OK** per aggiungere il gruppo padre.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     La formula assegna un numero a ogni set di 65000 righe nel set di dati. Se si definisce un'interruzione di pagina per il gruppo, si ottiene un'interruzione di pagina ogni 65000 righe.  
  
     Con l'aggiunta del gruppo di tabelle esterno viene aggiunta una colonna di gruppo al report.  
  
4.  Per eliminare la colonna di gruppo, fare clic con il pulsante destro del mouse sull'intestazione di colonna, fare clic su **Elimina colonne**, selezionare **Elimina solo colonne**, quindi scegliere **OK**.  
  
     ![Eliminare una colonna del gruppo](../media/groupcolumn-delete-updated.png "Eliminare una colonna del gruppo")  
  
5.  Fare clic con il pulsante destro del mouse su **Gruppo 1** nella sezione **Gruppi di righe** , quindi scegliere **Proprietà gruppo**.  
  
     ![Visualizzare le proprietà del gruppo](../media/groupproperties-updated.png "Visualizzare le proprietà del gruppo")  
  
6.  Nella pagina **Ordinamento** della finestra di dialogo **Proprietà gruppo** selezionare l'opzione di ordinamento predefinita e fare clic su **Elimina**.  
  
     ![Eliminare l'ordinamento predefinito](../media/groupproperties-sorting-updated.png "Eliminare l'ordinamento predefinito")  
  
7.  Nella pagina **Interruzioni di pagina** fare clic su **Tra ogni istanza di un gruppo** , quindi scegliere **OK**.  
  
     ![Impostare le interruzioni di pagina](../media/groupproperties-pagebreaks-updated.png "Impostare le interruzioni di pagina")  
  
8.  Salvare il report. Quando lo si esporta in Excel, viene esportato in più fogli di lavoro, ognuno con un massimo di 65000 righe.  
  
  
