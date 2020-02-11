---
title: Aggiungere, modificare o eliminare valori disponibili per un parametro di report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e9944e437be03dd7cfac3cbe6bad7c5224f3b462
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106682"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter-report-builder-and-ssrs"></a>Aggiungere, modificare o eliminare valori disponibili per un parametro di report (Generatore report e SSRS)
  Dopo aver creato un parametro del report, è possibile specificare un elenco di valori disponibili da visualizzare. Tale elenco limita le scelte dell'utente ai soli valori validi per il parametro.  
  
 I valori disponibili sono visualizzati durante l'esecuzione del report in un elenco a discesa della barra degli strumenti accanto al parametro di report. I parametri di report possono rappresentare un valore singolo o più valori. Per più valori, la funzionalità **Seleziona tutto** è disponibile all'inizio dell'elenco, in modo che l'utente possa selezionare o deselezionare tutti i valori con un solo clic.  
  
 È possibile fornire un elenco statico di valori o un elenco da un set di dati del report. È inoltre possibile fornire un nome descrittivo per i valori specificando un campo etichette. Per un parametro basato su un campo `ProductID` , è possibile ad esempio visualizzare il campo `ProductName` nell'etichetta del parametro. Durante l'esecuzione del report, è possibile scegliere i nomi di prodotto, ma il valore effettivo scelto è rappresentato dall'oggetto `ProductID`corrispondente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Dopo aver pubblicato un report, è possibile eseguire l'override dei valori disponibili definiti nel report nello strumento di creazione di report, impostando i valori delle proprietà del parametro nel server di report. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md).  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>Per aggiungere o modificare i valori disponibili per un parametro di report  
  
1.  Nel riquadro dei dati del report espandere il nodo Parametri. Fare clic con il pulsante destro del mouse sul parametro e scegliere **Proprietà parametri**. Verrà visualizzata la finestra di dialogo **Proprietà parametri report** .  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non è visualizzato, scegliere **Dati report** dal menu **Visualizza**.  
  
2.  Fare clic su **Valori disponibili**. Selezionare un'opzione relativa ai valori disponibili.  
  
    -   Fare clic su **Imposta valori** per fornire manualmente un elenco di valori. Facoltativamente, è possibile specificare i nomi descrittivi (etichette) per i valori.  
  
         Fare clic su **Aggiungi** e quindi immettere il valore nella casella di testo **Valore** . Facoltativamente, immettere anche l'etichetta nella casella di testo **Etichetta** . Se non si specifica un'etichetta verrà utilizzato il valore. È possibile scrivere un'espressione per un valore. Il tipo di dati deve corrispondere al tipo di dati del parametro. Non è possibile utilizzare i nomi di campi in un'espressione per un parametro. Per esempi, vedere [Filtri di uso comune &#40;Generatore report e SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md).  
  
         Ripetere questo passaggio per il numero desiderato di valori. Gli elementi vengono visualizzati nell'elenco a discesa in base all'ordine in cui appaiono nell'elenco. Per modificare l'ordine di un elemento nell'elenco, fare clic su una casella di testo **Valore** o **Etichetta** per selezionare l'elemento e quindi usare i pulsanti freccia per spostare l'elemento verso l'alto o verso il basso nell'elenco.  
  
    -   Fare clic su **Ottieni valori da una query** per specificare il nome di un set di dati esistente per il recupero di valori e, facoltativamente, i nomi descrittivi per il parametro.  
  
        > [!IMPORTANT]  
        >  Se nello stesso set di dati è contenuto il parametro di query corrispondente per il parametro di report, nel report verrà visualizzato un messaggio di errore quando si tenta di eseguirlo. Per risolvere l'errore, è necessario utilizzare un set di dati diverso per recuperare i valori.  
  
         In **Set di dati**scegliere il nome del set di dati.  
  
         In **Campo valori**scegliere il nome del campo in cui sono disponibili i valori del parametro.  
  
         In **Campo etichette**scegliere il nome del campo in cui sono disponibili i nomi descrittivi del parametro. Se non esiste un campo separato per i nomi descrittivi, scegliere lo stesso campo scelto per il campo **Valore** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nell'anteprima del report verrà visualizzato un elenco a discesa con i valori disponibili per il parametro.  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>Per rimuovere i valori disponibili per un parametro di report  
  
1.  Nel riquadro dei dati del report espandere il nodo Parametri. Fare clic con il pulsante destro del mouse sul parametro e scegliere **Proprietà parametri**. Verrà visualizzata la finestra di dialogo **Parametri report** .  
  
2.  Fare clic su **Valori disponibili**.  
  
3.  In **Selezionare una delle seguenti opzioni**fare clic su **Nessuno**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nell'anteprima del report l'elenco a discesa con i valori disponibili per il parametro non verrà più visualizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare valori predefiniti per un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
