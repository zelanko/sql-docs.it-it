---
title: Visualizzare le intestazioni di riga e colonna in più pagine (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cda91c882af3cead946a764ddd826e1291c5e18b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294950"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>Visualizzare le intestazioni di riga e colonna in più pagine (Generatore report e SSRS)
  È possibile specificare se ripetere le intestazioni di riga e di colonna in ogni pagina di un'area dati Tablix che si estende su più pagine. Un'area dati Tablix può essere una tabella, una matrice o un elenco.  
  
 La modalità di controllo di righe e colonne dipende dalla presenza o meno delle intestazioni di gruppo nell'area dati Tablix. Quando si fa clic in un'area dati Tablix che dispone di intestazioni di gruppo, una linea punteggiata indica le aree Tablix, come illustrato nella figura seguente:  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 Le intestazioni dei gruppi di righe e di colonne vengono create automaticamente quando si aggiungono gruppi tramite la procedura guidata Nuova tabella o matrice o Nuovo grafico, aggiungendo campi al riquadro Raggruppamento o tramite i menu di scelta rapida. Se nell'area dati Tablix è presente solo un'area del corpo della Tablix ma non sono disponibili intestazioni di gruppo, le righe e le colonne sono membri Tablix.  
  
 Per i membri statici, è possibile visualizzare le righe adiacenti superiori o le colonne adiacenti laterali in più pagine.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-row-headers-on-multiple-pages"></a>Per visualizzare le intestazioni di riga in più pagine  
  
1.  Fare clic con il pulsante destro del mouse sulla riga o sulla colonna oppure sull'handle d'angolo di un'area dati Tablix, quindi scegliere **Proprietà Tablix**.  
  
2.  In **Intestazioni riga**selezionare **Ripeti righe intestazione in ogni pagina**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-column-headers-on-multiple-pages"></a>Per visualizzare le intestazioni di colonna in più pagine  
  
1.  Fare clic con il pulsante destro del mouse sulla riga o sulla colonna oppure sull'handle d'angolo di un'area dati Tablix, quindi scegliere **Proprietà Tablix**.  
  
2.  In **Intestazioni colonna**selezionare **Ripeti colonne intestazione in ogni pagina**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-a-static-tablix-member-row-or-column-on-multiple-pages"></a>Per visualizzare un membro Tablix statico (riga o colonna) in più pagine  
  
1.  Nell'area di progettazione fare clic sull'handle di riga o di colonna dell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne.  
  
2.  Sul lato destro del riquadro di raggruppamento fare clic sulla freccia rivolta verso il basso, quindi fare clic su **Modalità avanzata**. Nel riquadro Gruppi di righe vengono visualizzati i membri statici e dinamici gerarchici per la gerarchia di gruppi di righe, mentre nel riquadro Gruppi di colonne è riportata una visualizzazione simile per la gerarchia di gruppi di colonne.  
  
3.  Fare clic sul membro statico che corrisponde al membro statico (riga o colonna) che si desidera mantenere visibile durante lo scorrimento. Nel riquadro Proprietà verranno visualizzate le proprietà dei **membri Tablix**.  
  
     Se il riquadro Proprietà non è visualizzato, fare clic sulla scheda **Visualizza** nella parte superiore della finestra di Generatore report, quindi scegliere **Proprietà**.  
  
4.  Nel riquadro Proprietà impostare **RepeatOnNewPage** su True.  
  
5.  Impostare **KeepWithGroup** su Dopo.  
  
6.  Ripetere questo passaggio per tutti i membri adiacenti che si desidera ripetere.  
  
7.  Visualizzare l'anteprima del report.  
  
 Durante la visualizzazione delle pagine del report incluse nell'area dati Tablix, i membri Tablix statici vengono ripetuti su ogni pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportazione di report &#40;Report e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [Controllo di interruzioni di pagina, intestazioni, colonne e righe &#40;Generatore report e SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Visualizzare intestazioni e piè di pagina con un gruppo &#40;Generatore report e SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Visualizzazione delle intestazioni durante lo scorrimento di un report &#40;Generatore report e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
