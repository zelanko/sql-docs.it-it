---
title: Creare un report con rientri (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de074a61bea0941b52240fe4d7b66eadc0cacaeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106125"
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>Creazione di un report con rientri (Generatore report e SSRS)
  In un report con rientri le righe di dettaglio oppure i gruppi figlio vengono visualizzati rientrati sotto un gruppo padre della stessa colonna, come illustrato nell'esempio seguente:  
  
 ![Rendering del report con rientri](../media/steppedreportrendered.gif "Rendering del report con rientri")  
  
 Nei tradizionali report tabella il gruppo padre viene inserito in una colonna adiacente del report. La nuova area dati Tablix consente di aggiungere un gruppo e righe di dettaglio o gruppi figlio alla stessa colonna. Per differenziare le righe di gruppo dalle righe di dettaglio o da quelle di gruppi figlio, è possibile applicare una formattazione, ad esempio il colore del carattere, o applicare il rientro alle righe di dettaglio.  
  
 Le procedure in questo argomento illustrano come creare manualmente un report avanzato, ma è anche possibile utilizzare la procedura guidata Nuova tabella/Matrice. Fornisce il layout per report con rientri, semplificandone la creazione. Dopo avere completato la procedura guidata, il report può essere ulteriormente migliorato.  
  
> [!NOTE]  
>  La procedura guidata è disponibile unicamente in Generatore report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-stepped-report"></a>Per creare un report con rientri  
  
1.  Creare un report tabella. Inserire ad esempio un'area dati Tablix e aggiungere campi alla riga di dati.  
  
2.  Aggiungere un gruppo padre al report.  
  
    1.  Fare clic in un punto qualsiasi della tabella per selezionarla. Nel riquadro di raggruppamento viene visualizzato il gruppo Dettagli presente nel riquadro Gruppi di righe.  
  
    2.  Nel riquadro di raggruppamento fare clic con il pulsante destro del mouse sul gruppo Dettagli, scegliere **Aggiungi gruppo**e quindi fare clic su **Gruppo padre**.  
  
    3.  Nella finestra di dialogo **Gruppo Tablix** specificare un nome per il gruppo e digitare o selezionare un'espressione di raggruppamento nell'elenco a discesa. Nell'elenco a discesa vengono visualizzate le espressioni di campo semplici disponibili nel riquadro dei dati del report. Ad esempio [PostalCode] è un'espressione di campo semplice per il campo PostalCode in un set di dati.  
  
    4.  Selezionare **Aggiungi intestazione gruppo**. Questa opzione consente di aggiungere una riga statica sopra il gruppo per l'etichetta e i totali relativi al gruppo stesso. Allo stesso modo è possibile selezionare **Aggiungi piè di pagina gruppo** per aggiungere una riga statica sotto il gruppo. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     A questo punto è disponibile un report tabella di base. Quando si esegue il rendering di tale report, verranno visualizzate una colonna con il valore dell'istanza del gruppo e una o più colonne con i dati di dettaglio raggruppati. Nella figura seguente viene illustrato il possibile aspetto dell'area dati nell'area di progettazione.  
  
     ![Area dati della tabella con gruppo](../media/tabledataregionwithgroup.gif "Area dati della tabella con gruppo")  
  
     Nelle figura seguente viene illustrato il possibile aspetto dell'area dati di cui è stato eseguito il rendering quando viene visualizzato il report.  
  
     ![Rendering di un report raggruppato](../media/tablereportrendered.gif "Rendering di un report raggruppato")  
  
3.  Per un report con rientri, non è necessario utilizzare la prima colonna in cui viene visualizzata l'istanza del gruppo, ma è necessario copiare il valore della cella dell'intestazione di gruppo, eliminare la colonna di gruppo e incollare il valore nella prima casella di testo della riga di intestazione di gruppo. Per rimuovere la colonna di gruppo, fare clic con il pulsante destro del mouse sulla colonna o la cella di gruppo e quindi scegliere **Elimina colonne**. Nella figura seguente viene illustrato il possibile aspetto dell'area dati nell'area di progettazione.  
  
     ![Area dati con riga di intestazione di gruppo](../media/tabledataregiongroupheader.gif "Area dati con riga di intestazione di gruppo")  
  
4.  Per applicare il rientro alle righe di dettaglio sotto la riga di intestazione di gruppo nella stessa colonna, modificare il riempimento della cella dei dati di dettaglio.  
  
    1.  Selezionare la cella con il campo di dettaglio per cui si desidera impostare il rientro. Le proprietà relative alla casella di testo per tale cella verranno visualizzate nel riquadro Proprietà.  
  
    2.  In **Allineamento**nel riquadro Proprietà espandere le proprietà relative a **Riempimento**.  
  
    3.  Per la **sinistra**, digitare un nuovo valore di spaziatura interna, ad esempio `.5in`. Il riempimento consente di applicare il rientro al testo presente nella cella in base al valore specificato. Il valore predefinito è 2 punti. Il valore valido per le proprietà relative a Riempimento è zero (0) oppure un numero positivo, seguito da un identificatore di dimensione.  
  
         Di seguito vengono riportati gli identificatori di dimensione:  
  
        |||  
        |-|-|  
        |`in`|Pollici (1 pollice = 2,54 centimetri)|  
        |`cm`|Centimetri|  
        |`mm`|Millimetri|  
        |`pt`|Punti (1 punto = 1/72 pollice)|  
        |`pc`|Pica (1 pica = 12 punti)|  
  
     L'aspetto dell'area dati sarà simile a quello riportato nell'esempio seguente.  
  
     ![Area dati per report con rientri](../media/steppedreportdataregion.gif "Area dati per report con rientri")  
  
     **Area dati per layout di report con rientri**  
  
     Nella scheda **Home** fare clic su **Esegui**. Nel report verrà visualizzato il gruppo con i livelli rientrati per i valori del gruppo figlio.  
  
### <a name="to-create-a-stepped-report-with-multiple-groups"></a>Per creare un report con rientri con più gruppi  
  
1.  Creare un report come descritto nella procedura precedente.  
  
2.  Aggiungere altri gruppi al report.  
  
    1.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul gruppo, scegliere **Aggiungi gruppo**e quindi il tipo di gruppo da aggiungere.  
  
        > [!NOTE]  
        >  È possibile aggiungere gruppi a un'area dati in modi diversi. Per altre informazioni, vedere [Aggiunta o eliminazione di un gruppo in un'area dati &#40;Generatore report e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
    2.  Nella finestra di dialogo **Gruppo Tablix** digitare un nome.  
  
    3.  In **Espressione di raggruppamento**digitare un'espressione o selezionare un campo del set di dati in base al quale eseguire il raggruppamento. Per creare un'espressione, fare clic sul pulsante Espressione (**fx**) per aprire la finestra di dialogo **Espressione** .  
  
    4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  Modificare il riempimento per la cella in cui vengono visualizzati i dati del gruppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
