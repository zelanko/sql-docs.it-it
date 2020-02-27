---
title: Aggiungere, modificare, aggiornare i campi nel riquadro Dati report (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c6bc3c94923c3ebdb6e2897c4d3aaedbc58621c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082577"
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report (Generatore report e SSRS)
  I campi del set di dati costituiscono la raccolta predefinita di nomi di campo che rappresentano i dati che vengono restituiti quando viene eseguita una query del set di dati in un'origine dati esterna.  
  
 Per un set di dati incorporato, i campi del set di dati sono i campi creati dopo che è stata completata la compilazione di una query, è stato chiuso il riquadro Progettazione query e sono stati calcolati i campi creati.  
  
 Per un set di dati condiviso, i campi del set di dati sono i campi della definizione del set di dati condiviso quando viene aggiunta al report in uso. Anche se la query del set di dati condiviso sul server di report viene utilizzata sempre durante l'esecuzione del report, l'elenco di campi del set di dati nel report è statico.  
  
 Utilizzare **Aggiorna campi** per aggiornare l'elenco di campi nel report affinché corrisponda all'elenco corrente di campi della query del set di dati condiviso. L'aggiornamento dell'elenco di campi non influisce sui campi calcolati definiti nel report in uso.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>Per aggiungere un campo di query  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse sul set di dati, quindi scegliere **Aggiungi campo query**.  
  
    > [!NOTE]  
    >  Se non è possibile visualizzare il riquadro Dati report, scegliere **Dati report** dal menu **Visualizza**.  
  
2.  Nella pagina **Campi** della finestra di dialogo **Proprietà set di dati** fare clic su **Aggiungi**, quindi scegliere **Campo query**. Verrà aggiunta una nuova riga nella parte inferiore della griglia.  
  
3.  Nella casella di testo **Nome campo** digitare il nome per il campo.  
  
    > [!NOTE]  
    >  I nomi devono essere univoci nell'ambito del set di dati.  
  
4.  Nella casella di testo **Origine campo** digitare il nome di un campo esistente nell'origine dati.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>Per aggiungere un campo calcolato  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse sul set di dati, quindi scegliere **Aggiungi campo calcolato**.  
  
2.  Nella pagina **Campi** della finestra di dialogo **Proprietà set di dati** fare clic su **Aggiungi**, quindi scegliere **Campo calcolato**. Verrà aggiunta una nuova riga nella parte inferiore della griglia.  
  
3.  Nella casella di testo **Nome campo** digitare il nome per il campo.  
  
    > [!NOTE]  
    >  I nomi devono essere univoci nell'ambito del set di dati.  
  
4.  Nella casella di testo **Origine campo** digitare l'espressione per il campo. Fare clic sul pulsante Espressione (**fx**) per compilare un'espressione.  
  
    > [!NOTE]  
    >  L'espressione per un campo calcolato non può contenere funzioni di aggregazione o riferimenti a elementi del report.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>Per modificare un campo di query o un campo del set di dati  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse sul campo, quindi scegliere **Proprietà campo**.  
  
2.  Nella pagina **Campi** della finestra di dialogo **Proprietà set di dati** fare clic su un campo esistente per selezionare la riga.  
  
3.  Modificare il nome o il valore del campo.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>Per eliminare un campo di query o un campo calcolato  
  
1.  Nel riquadro dei dati del report espandere il set di dati per visualizzare la raccolta di campi.  
  
2.  Fare clic con il pulsante destro del mouse sul campo che si desidera rimuovere, quindi scegliere **Elimina**.  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>Per aggiornare la raccolta di campi nel riquadro dei dati del report per il set di dati  
  
1.  Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sul set di dati e quindi scegliere **Query**.  
  
2.  Fare clic su **Aggiorna campi**.  
  
     Sul server di report viene eseguita la query del set di dati condiviso che restituisce la raccolta campi corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Strumenti di progettazione query in Reporting Services](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)   
 [Strumenti di progettazione query &#40;SSRS&#41;](query-design-tools-ssrs.md)  
  
  
