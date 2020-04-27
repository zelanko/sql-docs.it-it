---
title: Aggiungere, modificare o eliminare valori predefiniti per un parametro di report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10460"
- sql12.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c973f249a60b8a6180d5233604a9c372928d0a48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106667"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter-report-builder-and-ssrs"></a>Aggiungere, modificare o eliminare valori predefiniti per un parametro di report (Generatore report e SSRS)
  Dopo aver creato un parametro del report, è possibile specificare un elenco di valori predefiniti. Se tutti i parametri dispongono di un valore predefinito valido, il report viene eseguito automaticamente la prima volta che viene visualizzato o ne viene visualizzata l'anteprima.  
  
 I parametri di report possono rappresentare un valore singolo o più valori. Per i valori singoli, è possibile fornire un valore letterale o un'espressione, mentre per più valori è possibile fornire un elenco statico di valori o un elenco da un set di dati del report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Dopo aver pubblicato un report, è possibile eseguire l'override dei valori predefiniti definiti nel report nello strumento di creazione di report, impostando i valori delle proprietà del parametro nel server di report. Inoltre, per fornire più set di valori predefiniti del parametro, è possibile creare report collegati. Per altre informazioni, vedere  [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md)  
  
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
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
