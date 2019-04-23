---
title: Aggiunta di grafici sparkline e barre dei dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e84eef3df9122987ffb5d4e9125d2ae5397f15b4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59971217"
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>Aggiunta di grafici sparkline e barre dei dati (Generatore report e SSRS)
  I grafici sparkline e le barre dei dati sono grafici di riserva di piccole dimensioni contenenti numerose informazioni poco dettagliate. Per altre informazioni, vedere [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
 I grafici sparkline e le barre dei dati vengono posizionati generalmente nelle celle di una tabella o di una matrice. In ogni grafico sparkline di solito viene visualizzata una sola serie. Le barre dei dati possono includere più punti dati. L'influenza dei grafici sparkline e delle barre dei dati deriva dal ripetersi delle informazioni relative alla serie per ogni riga della tabella o matrice.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>Per aggiungere grafici sparkline o barre dei dati a una tabella o a una matrice  
  
1.  Se questa operazione non è già stata eseguita, creare una tabella o una matrice con i dati che si desidera visualizzare. Per altre informazioni, vedere [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md) o [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Inserire una colonna nella tabella o nella matrice. Per altre informazioni, vedere [Inserire o eliminare una colonna &#40;Generatore report e SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Scegliere **Grafico sparkline** o **Barra dei dati** nella scheda **Inserisci**e fare clic in una cella della nuova colonna.  
  
    > [!NOTE]  
    >  Non è possibile posizionare grafici sparkline in un gruppo di dettagli in una tabella. Devono essere inseriti in una cella associata a un gruppo.  
  
4.  Nella finestra di dialogo **Modifica tipo di grafico sparkline/barra dei dati** fare clic sul tipo di grafico sparkline o barra dei dati desiderato e quindi scegliere **OK**.  
  
5.  Scegliere il grafico sparkline o la barra dei dati.  
  
     Viene visualizzato il riquadro **Dati grafico** .  
  
6.  Nell'area **Valori** fare clic sul segno più ( **) di** Aggiungi campi**+** e selezionare il campo contenente i valori che si vuole inserire in formato grafico.  
  
7.  Nell'area **Gruppi di categorie** fare clic sul segno più ( **) di** Aggiungi campi**+** e selezionare il campo contenente i valori in base ai quali si vuole raggruppare.  
  
     In genere per i grafici sparkline e per le barre dei dati, non viene aggiunto un campo all'area **Gruppo serie** in quanto si desidera una sola serie per ogni riga.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Allineare i dati in un grafico di una tabella o matrice &#40;Generatore report e SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
