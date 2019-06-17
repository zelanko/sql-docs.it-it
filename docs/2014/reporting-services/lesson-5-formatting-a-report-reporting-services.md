---
title: 'Lezione 5: Formattazione di un report (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f1acd7bf033ca2170a2a2b0cb1f701606510bf14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108427"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lezione 5: Formattazione di un report (Reporting Services)
  Dopo avere aggiunto un'area dati e alcuni campi al report Sales Orders, è possibile formattare i campi relativi a data e valuta e le intestazioni di colonna.  
  
 Contenuto dell'argomento:  
  
-   [Formattare la data](#bkmk_format_date)  
  
-   [Formattare la valuta](#bkmk_format_currency)  
  
-   [Modifica dello stile di testo e la larghezza delle colonne](#bkmk_change_textstyle)  
  
##  <a name="bkmk_format_date"></a> Formattare la data  
 Nel campo Date vengono visualizzate la data e l'ora per impostazione predefinita. È possibile formattare tale campo in modo da visualizzare solo la data.  
  
#### <a name="to-format-a-date-field"></a>Per formattare un campo di tipo data  
  
1.  Fare clic sulla scheda **Progettazione** .  
  
2.  Fare clic con il pulsante destro del mouse nella cella contenente l'espressione per il campo `[Date]` e scegliere **Proprietà casella di testo**.  
  
3.  Fare clic su **numero**e quindi la **categoria** campo selezionare `Date`.  
  
4.  Nella casella **Tipo** selezionare **31 Gennaio 2000**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualizzare un'anteprima del report per vedere la modifica al campo `[Date]` , quindi tornare alla visualizzazione della struttura.  
  
##  <a name="bkmk_format_currency"></a> Formattare la valuta  
 Nel campo LineTotal viene visualizzato un numero generico. È possibile formattare tale numero come valuta.  
  
#### <a name="to-format-a-currency-field"></a>Per formattare un campo di tipo valuta  
  
1.  Fare clic con il pulsante destro del mouse nella cella contenente l'espressione per il campo `[LineTotal]` e scegliere **Proprietà casella di testo**.  
  
2.  Fare clic su **Numero**, quindi selezionare **Valuta** nel campo **Categoria**.  
  
3.  Se la lingua delle impostazioni locali è l'italiano, le impostazioni predefinite devono essere le seguenti:  
  
    -   **Cifre decimali: 2**  
  
    -   **Numeri negativi: (€12345,00)**  
  
    -   **Simbolo: € italiano**  
  
4.  Selezionare **Usa separatore delle migliaia (,)** .  
  
     Se il testo di esempio è: **$ 12.345,00**, le impostazioni sono corrette.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualizzare un'anteprima del report per vedere la modifica al campo `[LineTotal]` , quindi tornare alla visualizzazione della struttura.  
  
##  <a name="bkmk_change_textstyle"></a> Modifica dello stile di testo e la larghezza delle colonne  
 È possibile modificare anche la formattazione della riga dell'intestazione per differenziarla dalle righe di dati nel report. Come ultima operazione, si potrà regolare la larghezza delle colonne.  
  
#### <a name="to-format-header-rows-and-table-columns"></a>Per formattare le righe di intestazione e le colonne di tabella  
  
1.  Fare clic nella tabella in modo che vengano visualizzati gli handle di colonna e riga sopra e accanto alla tabella.  
  
     ![Progettazione, tabella con riga di intestazione e riga di dettaglio](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "progettazione, tabella con riga di intestazione e riga di dettaglio")  
  
     Le barre grigie lungo la parte superiore e laterale della tabella sono gli handle di riga e di colonna.  
  
2.  Posizionare il puntatore del mouse sulla riga tra gli handle di colonna in modo che il cursore assuma la forma di una doppia freccia. Trascinare le colonne fino a ottenere le dimensioni desiderate.  
  
3.  Selezionare la riga che contiene le etichette dell'intestazione di colonna e scegliere **Carattere** dal menu **Formato** , quindi fare clic su **Grassetto**.  
  
4.  Per visualizzare un'anteprima del report fare clic sulla scheda **Anteprima** . L'aspetto dell'anteprima dovrebbe essere simile al seguente:  
  
     ![Anteprima della tabella con intestazioni di colonna in grassetto](../../2014/tutorials/media/rs-basictabledetailsformattedpreview.gif "Anteprima della tabella con intestazioni di colonna in grassetto")  
  
5.  Per salvare il report, scegliere **Salva tutti** nel menu **File** .  
  
## <a name="next-steps"></a>Passaggi successivi  
 Sono stati formattati le intestazioni di colonna e i valori di data e valuta. È possibile aggiungere gruppi e totali al report. Vedere [Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
