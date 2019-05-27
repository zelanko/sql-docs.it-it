---
title: 'Lesson 5: Formatting a Report (Reporting Services) (Lezione 5: Formattazione di un report (Reporting Services)) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105932"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lezione 5: Formattazione di un report (Reporting Services)

Dopo avere aggiunto un'area dati e alcuni campi al report Sales Orders, è possibile formattare i campi relativi a data e valuta e le intestazioni di colonna.

## <a name="bkmk_format_date"></a>Formattare la data

Per impostazione predefinita, l'espressione del campo Date visualizza le informazioni di data e ora. È possibile formattare tale campo in modo da visualizzare solo la data.

1. Selezionare la scheda **Progettazione**.
2. Fare clic con il pulsante destro del mouse sulla cella contenente l'espressione del campo `[Date]` e quindi scegliere **Proprietà casella di testo**.
3. Selezionare **Numero** e quindi **Data** nel campo **Categoria**.
4. Nella casella **Tipo** selezionare **31 Gennaio 2000**.
5. Selezionare **OK** per applicare la formattazione.
6. Visualizzare l'anteprima del report per verificare la modifica della formattazione del campo `[Date]` e quindi tornare alla visualizzazione Progettazione.

## <a name="bkmk_format_currency"></a>Formattare la valuta

L'espressione del campo LineTotal visualizza un numero generico. È possibile formattare il campo in modo da visualizzare il numero come valuta.

1. Fare clic con il pulsante destro del mouse sulla cella contenente l'espressione `[LineTotal]` e scegliere **Proprietà casella di testo**.
2. Selezionare **Numero** nella casella di riepilogo della colonna più a sinistra e **Valuta** nella casella di riepilogo **Categoria**.
3. Se l'impostazione locale è Italiano (Italia), le impostazioni predefinite nella casella di riepilogo **Tipo** saranno le seguenti:
    - **Cifre decimali: 2**
    - **Numeri negativi: (€12345,00)**
    - **Simbolo: € italiano**
4. Selezionare **Usa separatore delle migliaia (,)**. Se il testo di esempio visualizzato è **€12.345,00**, le impostazioni sono corrette.
5. Selezionare **OK** per applicare la formattazione.
6. Visualizzare l'anteprima del report per verificare la modifica apportata alla colonna dell'espressione `[LineTotal]` e quindi tornare alla visualizzazione Progettazione.  

## <a name="bkmk_change_textstyle"></a>Modifica dello stile del testo e della larghezza delle colonne

È possibile formattare ulteriormente il report evidenziando la riga di intestazione e modificando la larghezza delle colonne di dati.

### <a name="to-format-header-rows-and-table-columns"></a>Per formattare le righe di intestazione e le colonne di tabella

1. Selezionare la tabella in modo da visualizzare gli handle di colonna e di riga sopra e accanto alla tabella. Le barre grigie lungo la parte superiore e laterale della tabella sono gli handle di riga e di colonna.

2. Posizionare il puntatore del mouse sulla riga tra gli handle di colonna in modo che il cursore assuma la forma di una doppia freccia. Trascinare le colonne fino a ottenere le dimensioni desiderate.
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. Selezionare la riga contenente le etichette di intestazione di colonna e scegliere **Carattere** > **Grassetto** dal menu **Formato**.

4. Visualizzare l'anteprima del report. L'aspetto dovrebbe essere il seguente:

    ![Anteprima della tabella con intestazioni di colonna in grassetto](media/rs-basictabledetailsformattedpreview.png "Anteprima della tabella con intestazioni di colonna in grassetto")  

5. Scegliere **Salva tutto** dal menu **File** per salvare il report.

## <a name="next-steps"></a>Passaggi successivi

In questa lezione sono state formattate le intestazioni di colonna e le espressioni dei campi. Verranno ora aggiunti raggruppamenti e totali al report. Passare a [Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md).

## <a name="see-also"></a>Vedere anche

[Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[Tipi di rendering &#40;Generatore report e SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
