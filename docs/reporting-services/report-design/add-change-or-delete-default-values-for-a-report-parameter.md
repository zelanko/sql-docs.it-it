---
title: Aggiungere, modificare o eliminare valori predefiniti per un parametro di report | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10460"
- sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a53bc057873f8c6905c37f281793c7d00c54a547
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293409"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter"></a>Aggiungere, modificare o eliminare valori predefiniti per un parametro di report
  Dopo aver creato un parametro del report, è possibile specificare un elenco di valori predefiniti. Se tutti i parametri dispongono di un valore predefinito valido, il report viene eseguito automaticamente la prima volta che viene visualizzato o ne viene visualizzata l'anteprima.  
  
 I parametri di report possono rappresentare un valore singolo o più valori. Per i valori singoli, è possibile fornire un valore letterale o un'espressione, mentre per più valori è possibile fornire un elenco statico di valori o un elenco da un set di dati del report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Dopo aver pubblicato un report, è possibile eseguire l'override dei valori predefiniti definiti nel report nello strumento di creazione di report, impostando i valori delle proprietà del parametro nel server di report. Inoltre, per fornire più set di valori predefiniti del parametro, è possibile creare report collegati. Per altre informazioni, vedere  [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>Per aggiungere o modificare i valori predefiniti per un parametro di report  
  
1.  Nel riquadro dei dati del espandere il nodo **Parametri** . Fare clic sul con il pulsante destro del mouse sul parametro, quindi scegliere **Modifica**. Verrà visualizzata la finestra di dialogo **Proprietà parametri report** .  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non è visualizzato, scegliere **Dati report** dal menu **Visualizza**.  
  
2.  Fare clic su **Valori predefiniti**.  
  
3.  Selezionare un'opzione predefinita:  
  
    -   Per fornire manualmente un valore o un elenco di valori, fare clic su **Imposta valori**. Fare clic su **Aggiungi** , quindi immettere il valore nella casella di testo **Valore** . È possibile scrivere un'espressione per un valore. Il tipo di dati deve corrispondere al tipo di dati del parametro. Non è possibile utilizzare i nomi di campi in un'espressione per un parametro.  
  
         Per i parametri multivalore, ripetere questo passaggio per il numero desiderato di valori. Gli elementi vengono visualizzati nell'elenco a discesa in base all'ordine in cui appaiono nell'elenco. Per modificare l'ordine di un elemento nell'elenco, fare clic su una casella di testo **Valore** per selezionare l'elemento, quindi usare i pulsanti freccia per spostare l'elemento verso l'alto o verso il basso nell'elenco.  
  
    -   Per fornire il nome di un set di dati che recupera i valori, fare clic su **Ottieni valori da una query**. In **Set di dati**scegliere il nome del set di dati.  
  
         In **Campo valori**scegliere il nome del campo in cui sono disponibili i valori del parametro.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>Per rimuovere i valori predefiniti per un parametro di report  
  
1.  Nel riquadro dei dati del espandere il nodo **Parametri** . Fare clic sul con il pulsante destro del mouse sul parametro, quindi scegliere **Modifica**. Verrà visualizzata la finestra di dialogo **Proprietà parametri report** .  
  
2.  Fare clic su **Valori predefiniti**.  
  
3.  In **Selezionare una delle seguenti opzioni**fare clic su **Nessun valore predefinito**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
