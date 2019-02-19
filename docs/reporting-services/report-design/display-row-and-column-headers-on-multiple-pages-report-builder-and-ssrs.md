---
title: Visualizzare le intestazioni di riga e colonna in più pagine (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ad0da97b8b9837213a0abff73204a2287b02e011
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291989"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>Visualizzare le intestazioni di riga e colonna in più pagine (Generatore report e SSRS)
  È possibile specificare se ripetere le intestazioni di riga e di colonna in ogni pagina di report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] per un'area dati Tablix (tabella, matrice o elenco) che si estende su più pagine.
  
 La modalità di controllo di righe e colonne dipende dalla presenza o meno delle intestazioni di gruppo nell'area dati Tablix. Quando si fa clic in un'area dati Tablix che dispone di intestazioni di gruppo, una linea punteggiata indica le aree Tablix, come illustrato nella figura seguente:  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 Le intestazioni dei gruppi di righe e di colonne vengono create automaticamente quando si aggiungono gruppi tramite la procedura guidata Nuova tabella o matrice o Nuovo grafico, aggiungendo campi al riquadro Raggruppamento o tramite i menu di scelta rapida. Se nell'area dati Tablix è presente solo un'area del corpo della Tablix ma non sono disponibili intestazioni di gruppo, le righe e le colonne sono membri Tablix.  
  
 Per i membri statici, è possibile visualizzare le righe adiacenti superiori o le colonne adiacenti laterali in più pagine.  
  
## <a name="to-display-row-headers-on-multiple-pages"></a>Per visualizzare le intestazioni di riga in più pagine  
  
1.  Fare clic con il pulsante destro del mouse sulla riga o sulla colonna oppure sull'handle d'angolo di un'area dati Tablix, quindi scegliere **Proprietà Tablix**.  
  
2.  In **Intestazioni riga**selezionare **Ripeti righe intestazione in ogni pagina**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-column-headers-on-multiple-pages"></a>Per visualizzare le intestazioni di colonna in più pagine  
  
1.  Fare clic con il pulsante destro del mouse sulla riga o sulla colonna oppure sull'handle d'angolo di un'area dati Tablix, quindi scegliere **Proprietà Tablix**.  
  
2.  In **Intestazioni colonna**selezionare **Ripeti colonne intestazione in ogni pagina**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-a-static-row-or-column-on-multiple-pages"></a>Per visualizzare una riga o una colonna statica in più pagine  
  
1.  Nell'area di progettazione fare clic sull'handle di riga o di colonna dell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne.  
  
2.  Sul lato destro del riquadro di raggruppamento fare clic sulla freccia rivolta verso il basso, quindi fare clic su **Modalità avanzata**. Nel riquadro Gruppi di righe vengono visualizzati i membri statici e dinamici gerarchici per la gerarchia di gruppi di righe, mentre nel riquadro Gruppi di colonne è riportata una visualizzazione simile per la gerarchia di gruppi di colonne.  
  
3.  Fare clic sul membro statico che corrisponde al membro statico (riga o colonna) che si desidera mantenere visibile durante lo scorrimento. Nel riquadro Proprietà verranno visualizzate le proprietà dei **membri Tablix** .  
  
     Se il riquadro Proprietà non è visualizzato, fare clic sulla scheda **Visualizza** nella parte superiore della finestra di Generatore report, quindi scegliere **Proprietà**.  
  
4.  Nel riquadro Proprietà impostare **RepeatOnNewPage** su True.  
  
5.  Impostare **KeepWithGroup** su Dopo.  
  
6.  Ripetere questo passaggio per tutti i membri adiacenti che si desidera ripetere.  
  
7.  Visualizzare l'anteprima del report.  
  
 Durante la visualizzazione delle pagine del report incluse nell'area dati Tablix, i membri Tablix statici vengono ripetuti su ogni pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Controllo di interruzioni di pagina, intestazioni, colonne e righe &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Visualizzare intestazioni e piè di pagina con un gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Visualizzazione delle intestazioni durante lo scorrimento di un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
