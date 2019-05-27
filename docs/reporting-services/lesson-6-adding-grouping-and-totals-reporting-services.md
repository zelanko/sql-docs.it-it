---
title: 'Lesson 6: Adding Grouping and Totals (Reporting Services) (Lezione 6: Aggiunta di gruppi e totali (Reporting Services)) | Microsoft Docs'
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5b9846a20615cf613dd50752ac63f2669b1e399
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089672"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)

In questa lezione finale dell'esercitazione si aggiungeranno raggruppamenti e totali al report [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per organizzare e riepilogare i dati.  

## <a name="to-group-data-in-a-report"></a>Per raggruppare i dati di un report

1. Selezionare la scheda **Progettazione**.
2. Se il riquadro **Gruppi di righe** non è visualizzato, fare clic con il pulsante destro del mouse sull'area di progettazione e scegliere **Visualizza** >**Raggruppamento**.
3. Dal riquadro **Dati report** trascinare il campo `[Date]` nel riquadro **Gruppi di righe**. Posizionarlo sopra la riga in cui è visualizzato **= (Dettagli)**.

    > [!NOTE]
    > Si noti che nell'handle di riga è ora presente una parentesi, che indica un gruppo. La tabella contiene ora due colonne con l'espressione `[Date]`, una su ogni lato di una linea verticale tratteggiata.
    >
    >![gruppo data aggiunto](media/rs-basictablegroups1design.png "gruppo data aggiunto")
4. Dal riquadro **Dati report** trascinare il campo `[Order]` nel riquadro **Gruppi di righe**. Posizionarlo sotto **Date** e sopra **= (Dettagli)**.

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > Si noti che nell'handle di riga sono ora presenti due parentesi (![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png)), che indicano due gruppi. La tabella contiene ora due colonne con l'espressione `[Order]`.

5. Eliminare le colonne con le espressioni `[Date]` e `[Order]` originali a destra della linea doppia. Selezionare gli handle delle due colonne, fare clic con il pulsante destro del mouse e scegliere **Elimina colonne**. Progettazione report rimuoverà le espressioni delle righe singole, in modo da visualizzare solo le espressioni di raggruppamento.

    ![Selezionare le colonne da eliminare](media/rs-basictablegroupsdeletecols.gif "Selezionare colonne da eliminare")

6. Per formattare la nuova colonna `[Date]`, fare clic con il pulsante destro del mouse sulla cella dell'area dati contenente l'espressione `[Date]` e scegliere **Proprietà casella di testo**.
7. Selezionare **Numero** nella casella di riepilogo della colonna più a sinistra e **Data** nella casella di riepilogo **Categoria**.
8. Nella casella di riepilogo **Tipo** selezionare **31 gennaio 2000**.
9. Selezionare **OK** per applicare la formattazione.
10. Visualizzare di nuovo l'anteprima del report. L'aspetto dovrebbe essere il seguente:

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>Aggiunta di totali a un report

1. Passare alla visualizzazione **Progettazione**.
2. Fare clic con il pulsante destro del mouse sulla cella dell'area dati contenente l'espressione `[LineTotal]` e scegliere **Aggiungi totale**. Progettazione report aggiungerà una riga con la somma dell'importo di ogni ordine.
3. Fare clic con il pulsante destro del mouse sulla cella contenente il campo `[Qty]` e scegliere **Aggiungi totale**. Progettazione report aggiungerà la somma della quantità di ogni ordine alla riga dei totali.
4. Nella cella vuota a sinistra della cella `Sum[Qty]` digitare la stringa "Order Total".
5. È possibile aggiungere un colore di sfondo alla riga dei totali. Selezionare le due celle della somma e la cella dell'etichetta.  
6. Scegliere **Colore di sfondo** > quadrato **Grigio chiaro** dal menu **Formato**.
7. Selezionare **OK** per applicare la formattazione.

   ![Visualizzazione progettazione: tabella di base con totale degli ordini](media/rs-basictablesumlinetotaldesign.gif "Visualizzazione progettazione: tabella semplice con totale degli ordini")

## <a name="add-the-daily-total-to-the-report"></a>Aggiungere il totale giornaliero al report

1. Fare clic con il pulsante destro del mouse sulla cella con l'espressione `[Order]` e scegliere **Aggiungi totale** > **Dopo**. Progettazione report aggiungerà una nuova riga contenente le somme dei valori `[Qty]` e `[Linetotal]` per ogni giorno e la stringa "Total" in fondo alla colonna dell'espressione `[Order]`.
2. Digitare la parola "Daily" prima di "Total" nella stessa cella in modo da ottenere "Daily Total".
3. Selezionare la cella, le due celle adiacenti dei totali sulla destra e la cella vuota in mezzo.
4. Scegliere **Colore di sfondo** > quadrato **Arancione** dal menu **Formato**.
5. Selezionare **OK** per applicare la formattazione.

   ![Impostare il colore di sfondo su arancione](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>Aggiungere il totale complessivo al report

1. Fare clic con il pulsante destro del mouse sulla cella con l'espressione `[Date]` e scegliere **Aggiungi totale** > **Dopo**. Progettazione report aggiungerà una nuova riga contenente le somme dei valori `[Qty]` e `[LineTotal]` per l'intero report e la stringa "Total" in fondo alla colonna dell'espressione `[Date]`.
2. Digitare la parola "Grand" prima di "Total" nella stessa cella in modo da ottenere "Grand Total".
3. Selezionare la cella con "Grand Total", le due celle con l'espressione `Sum()` e le celle vuote in mezzo.
4. Scegliere **Colore di sfondo** > quadrato **Azzurro** dal menu **Formato**.
5. Selezionare **OK** per applicare la formattazione.

    ![Visualizzazione progettazione: totale complessivo nella tabella semplice](media/rs-basictablesumgrandtotaldesign.gif "visualizzazione progettazione: totale complessivo nella tabella semplice")

## <a name="preview-the-report"></a>Visualizzare l'anteprima del report

Per visualizzare in anteprima le modifiche apportate alla formattazione, selezionare la scheda **Anteprima**. Sulla barra degli strumenti **Anteprima** selezionare il pulsante **Ultima pagina**, visualizzato come ![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png). I risultati dovrebbero avere l'aspetto seguente:

   ![Anteprima: tabella semplice con totale complessivo](media/rs-basictablesumgrandtotalpreview.gif "Anteprima: tabella semplice con totale complessivo")

## <a name="publishing-the-report-to-the-report-server-optional"></a>Pubblicazione del report nel *server di report* (facoltativo)

Un passaggio facoltativo consiste nel pubblicare il report completato nel server di report in modo da consentirne la visualizzazione nel portale Web.

1. Scegliere **Proprietà Tutorial** dal menu **Progetto**.
2. In **TargetServerURL** digitare il nome del server di report in uso, ad esempio:
    - `http:/<servername>/reportserver`
    - `https://localhost/reportserver` funziona se la progettazione del report viene eseguita nel server di report.

3. Il nome di **TargetReportFolder** è Tutorial, dal nome del progetto. Progettazione report distribuisce il report in questa cartella.
4. Fare clic su **OK**.
5. Scegliere **Distribuisci Tutorial** dal menu **Compila**.

    Se viene visualizzato un messaggio simile al seguente nella finestra **Output**, la distribuzione è stata completata correttamente.

    > ------ Compilazione avviata: Progetto: tutorial, Configurazione: Debug ------  
    > 'Sales Orders.rdl' verrà ignorato. L'elemento è aggiornato.  
    > Compilazione completata -- 0 errori, 0 avvisi  
    > ------ Distribuzione avviata: Progetto: tutorial, Configurazione: Debug ------  
    > È in corso la distribuzione in `https://[server name]/reportserver`  
    > Distribuzione report '/tutorial/Sales Orders'.  
    > Distribuzione completata -- 0 errori, 0 avvisi  
    > ========== Compilazione: 1 completate o aggiornate, 0 non riuscite, 0 ignorate ==========  
    > ========== Distribuzione: 1 completate, 0 non riuscite, 0 ignorate ==========  

    Se viene visualizzato un messaggio di errore simile al seguente, verificare di avere le autorizzazioni appropriate per il server di report e di aver avviato [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] con privilegi di amministratore.
    >
    > "Le autorizzazioni concesse all'utente 'XXXXXXXX\\&lt;nome utente&gt;' non sono sufficienti per eseguire questa operazione"

6. Aprire un browser con privilegi di amministratore. Ad esempio, fare clic con il pulsante destro del mouse sull'icona di Internet Explorer e scegliere **Esegui come amministratore**.
7. Individuare l'URL del portale Web.
   - `https://<server name>/reports`.
   - `https://localhost/reports` funziona se la progettazione del report viene eseguita nel server di report.

8. Selezionare la cartella Tutorial e quindi il report "Sales Orders" per visualizzarlo.

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

L'esercitazione **Creare un report tabella semplice** è stata completata.

## <a name="see-also"></a>Vedere anche

[Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
