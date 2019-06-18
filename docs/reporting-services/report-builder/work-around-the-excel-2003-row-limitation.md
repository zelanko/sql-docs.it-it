---
title: Ovviare alla limitazione di righe di Excel 2003 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3898e4202d958c1d20d5436a143e80bb45c7490f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65577788"
---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  In questo argomento viene illustrato come risolvere il limite di righe di Excel 2003 quando si esportano i report impaginati in Excel. La soluzione alternativa consiste in un report contenente una sola tabella.  
  
> [!IMPORTANT]  
>  L'estensione per il rendering di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 è deprecata. Per altre informazioni, vedere [Funzionalità deprecate di SQL Server Reporting Services in SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Excel 2003 supporta un massimo di 65.536 righe per foglio di lavoro. È possibile risolvere questo limite forzando un'interruzione di pagina esplicita dopo un determinato numero di righe. Tramite il renderer Excel viene creato un nuovo foglio di lavoro per ogni interruzione di pagina esplicita.  
  
### <a name="to-create-an-explicit-page-break"></a>Per creare un'interruzione di pagina esplicita  
  
1.  Aprire il report in [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] o nel portale Web [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Fare clic con il pulsante destro del mouse sulla riga dei dati nella tabella, quindi scegliere **Aggiungi gruppo** > **Gruppo padre** per aggiungere un gruppo di tabelle esterno.  
  
     ![Selezionare Gruppo padre](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "Selezionare Gruppo padre")  
  
3.  Immettere la formula seguente nella casella dell'espressione **Raggruppa per** , quindi fare clic su **OK** per aggiungere il gruppo padre.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     La formula assegna un numero a ogni set di 65000 righe nel set di dati. Se si definisce un'interruzione di pagina per il gruppo, si ottiene un'interruzione di pagina ogni 65000 righe.  
  
     Con l'aggiunta del gruppo di tabelle esterno viene aggiunta una colonna di gruppo al report.  
  
4.  Per eliminare la colonna di gruppo, fare clic con il pulsante destro del mouse sull'intestazione di colonna, fare clic su **Elimina colonne**, selezionare **Elimina solo colonne**, quindi scegliere **OK**.  
  
     ![Eliminare una colonna del gruppo](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "Eliminare una colonna del gruppo")  
  
5.  Fare clic con il pulsante destro del mouse su **Gruppo 1** nella sezione **Gruppi di righe** , quindi scegliere **Proprietà gruppo**.  
  
     ![Visualizzare le proprietà del gruppo](../../reporting-services/report-builder/media/groupproperties-updated.png "Visualizzare le proprietà del gruppo")  
  
6.  Nella pagina **Ordinamento** della finestra di dialogo **Proprietà gruppo** selezionare l'opzione di ordinamento predefinita e fare clic su **Elimina**.  
  
     ![Eliminare l'ordinamento predefinito](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "Eliminare l'ordinamento predefinito")  
  
7.  Nella pagina **Interruzioni di pagina** fare clic su **Tra ogni istanza di un gruppo** , quindi scegliere **OK**.  
  
     ![Impostare le interruzioni di pagina](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "Impostare le interruzioni di pagina")  
  
8.  Salvare il report. Quando lo si esporta in Excel, viene esportato in più fogli di lavoro, ognuno con un massimo di 65000 righe.  
  
  
