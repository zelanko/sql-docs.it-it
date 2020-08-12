---
title: Personalizzare il riquadro dei parametri in un report (Generatore report) | Microsoft Docs
description: Informazioni su come personalizzare il riquadro Parametri quando si creano report impaginati con parametri in Generatore report.
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796562"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Customize the Parameters Pane in a Report (Report Builder)
  Quando si creano report impaginati con parametri in Generatore report, è possibile personalizzare il riquadro Parametri. Nella visualizzazione di progettazione report è possibile trascinare un parametro in una colonna e in una riga specifiche del riquadro Parametri. È possibile aggiungere e rimuovere colonne per modificare il layout del riquadro.

 Quando si trascina un parametro in una nuova colonna e riga del riquadro, l'ordine del parametro nel riquadro **Dati report** viene modificato. Quando si modifica l'ordine del parametro nel riquadro **Dati report** , viene modificata la posizione del parametro stesso nel riquadro. Per informazioni sul motivo per cui l'ordine dei parametri è importante, vedere [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).

## <a name="to-customize-the-parameters-pane"></a>Per personalizzare il riquadro dei parametri

1.  Nella scheda **Vista** selezionare la casella di controllo **Parametri** per visualizzare il riquadro dei parametri.

     ![Accedere al riquadro Parametri dalla scheda Visualizza](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "Accedere al riquadro Parametri dalla scheda Visualizza")

     Il riquadro viene visualizzato nella parte superiore dell'area di progettazione.

2.  Per aggiungere un parametro al riquadro, eseguire una delle operazioni seguenti.

    -   Fare clic con il pulsante destro del mouse su una cella vuota nel riquadro dei parametri e quindi scegliere **Aggiungi parametro**.

         ![Aggiungere il nuovo parametro dal riquadro Parametri](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "Aggiungere il nuovo parametro dal riquadro Parametri")

    -   Fare clic con il pulsante destro del mouse su **Parametri** nel riquadro **Dati report** e quindi scegliere **Aggiungi parametro**.

3.  Per spostare un parametro in una nuova posizione nel riquadro dei parametri, trascinare il parametro in una cella diversa del riquadro.

     Quando si modifica la posizione del parametro nel riquadro, viene automaticamente modificato l'ordine del parametro nell'elenco **Parametri** del riquadro **Dati report** . Per altre informazioni sull'impatto dell'ordine dei parametri, vedere [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)

4.  Per accedere alle proprietà di un parametro, eseguire una delle operazioni seguenti.

    -   Fare clic con il pulsante destro del mouse sul riquadro dei parametri, quindi scegliere **Proprietà parametri**.

         ![Accedere alle proprietà dei parametri dal riquadro Parametri](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "Accedere alle proprietà dei parametri dal riquadro Parametri")

    -   Fare clic con il pulsante destro del mouse sul riquadro **Dati report** e quindi scegliere **Proprietà parametri**.

5.  Per aggiungere nuove colonne e righe al riquadro o eliminare le colonne e le righe esistenti, fare clic con il pulsante destro del mouse in un punto qualsiasi del riquadro dei parametri e quindi selezionare un comando nel menu visualizzato.

     ![Aggiungere colonne e righe al riquadro Parametri](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "Aggiungere colonne e righe al riquadro Parametri")

    > [!IMPORTANT]
    >  Quando si elimina una colonna o una riga contenente parametri, questi vengono eliminati dal report.

6.  Per eliminare un parametro dal riquadro e dal report, eseguire una delle operazioni seguenti.

    -   Fare clic con il pulsante destro del mouse sul riquadro dei parametri, quindi scegliere  **Elimina**.

         ![Eliminare parametri dal riquadro Parametri](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "Eliminare parametri dal riquadro Parametri")

    -   Fare clic con il pulsante destro del mouse sul riquadro **Dati report** e quindi scegliere **Elimina**.

## <a name="hiddeninternal-parameters-during-runtime"></a>Parametri nascosti/interni in runtime
Se si ha un parametro nascosto/interno, la logica che stabilisce se questo verrà visualizzato come spazio vuoto in runtime è la seguente:

   - Se una riga o una colonna contiene solo parametri nascosti/interni o celle vuote, in runtime il rendering dell'intera riga o colonna non verrà eseguito
   - In caso contrario, per il parametro nascosto/interno o la cella vuota verrà eseguito il rendering come spazio vuoto

`ReportParameter1`, ad esempio, è nascosto, mentre il resto dei parametri è visibile:

![Esempio di parametro nascosto 1](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "Un parametro nascosto nella griglia di layout")

In runtime il risultato è uno spazio vuoto perché sono presenti parametri visibili nella prima colonna o nella prima riga:

![Esempio di parametro nascosto 1 - runtime](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "Un parametro nascosto nella griglia di layout risultante in uno spazio vuoto in runtime")

Nello stesso esempio, se si imposta anche `ReportParameter3` come nascosto:

![Esempio di parametro nascosto 2](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "Due parametri nascosti nella stessa colonna")

In runtime non viene eseguito il rendering della prima colonna in fase di esecuzione perché l'intera colonna viene considerata vuota:

![Esempio di parametro nascosto 2 - runtime](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "Due parametri nascosti nella stessa colonna in runtime")

## <a name="default-layout"></a>Layout predefinito
Per i report creati prima di SQL Server Reporting Services 2016, in runtime viene usata una griglia di layout dei parametri predefinita di 2 colonne e N righe. Per modificare il layout predefinito, aprire il report in Generatore report di Microsoft e salvare il report. Dopo aver salvato il report, le informazioni sul layout dei parametri personalizzato verranno salvate nel file con estensione rdl.


## <a name="see-also"></a>Vedere anche
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


