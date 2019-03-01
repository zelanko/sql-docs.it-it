---
title: 'Lezione 6: Aggiunta di gruppi e totali (Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24d21ae735b44a7068ca929515b66e8a33aade8d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290079"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lezione 6: Aggiunta di gruppi e totali (Reporting Services)
In questa lezione dell'esercitazione verranno aggiunti raggruppamenti e totali al report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per organizzare e riepilogare i dati.  
  
  
## <a name="bkmk_groupdata"></a>Per raggruppare i dati di un report  
  
1.  Fare clic sulla scheda **Progettazione** .  
  
2.  Se il riquadro **Gruppi di righe** non è visualizzato, fare clic con il pulsante destro del mouse sull'area di progettazione e selezionare **Visualizza** e quindi scegliere **Raggruppamento**.  
  
3.  Dal riquadro dei **dati del report** trascinare il campo **Date** nel riquadro **Gruppi di righe** . Posizionarlo al di sopra della riga **(Dettagli)**.
  
    L'handle di riga contiene ora una parentesi quadra per mostrare un gruppo. La tabella presenta ora due colonne Date, una su ogni lato di una linea verticale tratteggiata.  
  
    ![gruppo data aggiunto](../reporting-services/media/rs-basictablegroups1design.png "gruppo data aggiunto")  
  
4.  Dal riquadro dei **dati del report** trascinare il campo **Order** nel riquadro **Gruppi di righe** . Posizionarlo al di sotto di Date e al di sopra di **(Dettagli)**.

    ![ssrs_ssdt_addorderfield](../reporting-services/media/ssrs-ssdt-addorderfield.png)   
  
    L'handle di riga contiene ora due parentesi quadre al suo interno ![ssrs_ssdt_rowgroupdoublehandles](../reporting-services/media/ssrs-ssdt-rowgroupdoublehandles.png) per mostrare due gruppi. La tabella ora presenta anche due colonne **Order** .  
  
5.  Eliminare le colonne **Date** e **Order** originali a **destra** della linea doppia. Verranno rimossi i singoli valori dei record in modo da visualizzare solo il valore del gruppo. Selezionare gli handle delle due colonne, fare clic con il pulsante destro del mouse e scegliere **Elimina colonne**.  
  
    ![Selezionare le colonne da eliminare](../reporting-services/media/rs-basictablegroupsdeletecols.gif "Selezionare colonne da eliminare")  
  
6.  Fare clic con il pulsante destro del mouse nella cella contenente l'espressione per il campo `[Date]` e scegliere **Proprietà casella di testo**.  
  
7.  Fare clic su **Numero**, quindi selezionare **Data** nel campo **Categoria**.  
  
8.  Nella casella **Tipo** selezionare **31 Gennaio 2000**.  
  
9.  [!INCLUDE[clickOK](../includes/clickok-md.md)].  
  
10.  Per visualizzare un'anteprima del report, passare alla scheda **Anteprima** . Il risultato dovrebbe essere simile a quanto illustrato nella figura seguente:  
    ![rs_BasicTableGroupsPreview](../reporting-services/media/rs-basictablegroupspreview.png) 
  
## <a name="bkmk_addtotals"></a>Per aggiungere totali a un report  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic con il pulsante destro del mouse sulla cella dell'area dati contenente il campo `[LineTotal]`e fare clic su **Aggiungi totale**.  
  
    Verrà aggiunta una riga con una somma degli importi di tutti gli ordini.  
  
3.  Fare clic con il pulsante destro del mouse sulla cella contenente il campo `[Qty]`e fare clic su **Aggiungi totale**.  
  
    Verrà aggiunta una somma delle quantità di tutti gli ordini alla riga dei totali.  
  
4.  Nella cella vuota a sinistra di `Sum[Qty]`digitare l'etichetta "**Order Total"**.  
  
5.  È possibile aggiungere un colore di sfondo alla riga dei totali. Selezionare le due celle della somma e la cella dell'etichetta.  
  
6.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Grigio chiaro**e scegliere **OK**.  
  
    ![Visualizzazione Progettazione: tabella di base con totale degli ordini](../reporting-services/media/rs-basictablesumlinetotaldesign.gif "Visualizzazione Progettazione: tabella di base con totale degli ordini")  
  
## <a name="bkmk_adddailytotal"></a>Per aggiungere un totale giornaliero a un report  
  
1.  Fare clic con il pulsante destro del mouse sulla cella **Order** , scegliere **Aggiungi totale**e quindi fare clic su **Dopo**.  
  
    Verrà aggiunta una nuova riga che contiene le somme delle quantità e degli importi di tutti i giorni e l'etichetta "**Total**" nella colonna Order.  
  
2.  Digitare la parola **Daily** prima della parola **Total** nella stessa cella in modo da definire la frase **Daily Total**.  
  
3.  Selezionare la cella **Daily Total** , le due celle **Sum** e la cella vuota compresa tra di esse.  
  
4.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Arancione**e scegliere **OK**.  
  
    ![Impostare il colore di sfondo su arancione](../reporting-services/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
## <a name="bkmk_addgrandtotal"></a>Per aggiungere un totale complessivo a un report  
  
1.  Fare clic con il pulsante destro del mouse sulla cella Date, scegliere **Aggiungi totale**e quindi fare clic su **Dopo**.  
  
    Verrà aggiunta una nuova riga che contiene le somme delle quantità e degli importi dell'intero report e l'etichetta **Total** nella colonna **Date** .  
  
2.  Digitare la parola **Grand** prima della parola **Total** nella stessa cella in modo da definire la frase **Grand Total**.  
  
3.  Selezionare la cella **Grand Total** , le due celle **Sum** e le celle vuote comprese tra di esse.  
  
4.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Azzurro**e scegliere **OK**.  
  
    ![Visualizzazione Progettazione: totale complessivo in una tabella di base](../reporting-services/media/rs-basictablesumgrandtotaldesign.gif "Visualizzazione Progettazione: totale complessivo in una tabella di base")  
  
5.  Fare clic su **Anteprima**.  
  
    L'ultima pagina dovrebbe essere simile all'immagine seguente. Nella barra degli strumenti fare clic su Ultima pagina ![ssrs_ssdt_viewertoolbar_lastpage](../reporting-services/media/ssrs-ssdt-viewertoolbar-lastpage.png).   
  
    ![Anteprima: tabella di base con totale complessivo](../reporting-services/media/rs-basictablesumgrandtotalpreview.gif "Anteprima: tabella di base con totale complessivo")  
  
## <a name="bkmk_publishreport"></a>Per pubblicare il report nel server di report (facoltativo)  
  
1.  Un passaggio facoltativo consiste nel pubblicare il report completato nel server di report in modalità nativa in modo che sia possibile visualizzare il report nel portale Web.  
  
2.  Fare clic sul menu **Progetto** e quindi su **Proprietà tutorial...**  
  
3.  In **TargetServerURL** digitare il nome del server di report in uso, ad esempio   
    - `http:/<servername>/reportserver`  
   
    - `https://localhost/reportserver` funziona se la progettazione del report viene eseguita nel server di report.  
  
  
4. Si noti che TargetReportFolder è l'esercitazione, il nome del progetto.  Questo è il nome della cartella in cui il report verrà distribuito nei passaggi successivi.  
5. Fare clic su **OK**.  
  
6.  Scegliere **Distribuisci Tutorial** dal menu **Compila**.  
  
    Se viene visualizzato un messaggio simile al seguente nella finestra di output, la distribuzione è stata completata correttamente.  
  
    > ------ Compilazione avviata - Progetto: tutorial, Configurazione: Debug ------  
    > 'Sales Orders.rdl' verrà ignorato. L'elemento è aggiornato.  
    > Compilazione completata -- 0 errori, 0 avvisi  
    > ------ Stato distribuzione: Progetto: tutorial, Configurazione: Debug ------  
    > Distribuzione in https://[nome server]/reportserver  
    > Distribuzione report '/tutorial/Sales Orders'.  
    > Distribuzione completata -- 0 errori, 0 avvisi  
    > ========== Compilazione: 1 completate o aggiornate, 0 non riuscite, 0 ignorate ==========  
    > ========== Distribuzione: 1 completata, 0 non riuscite, 0 ignorate ==========  
  
    Se viene visualizzato un messaggio di errore simile al seguente, verificare di disporre delle autorizzazione per il server di report e di aver avviato [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] con privilegi di amministratore.  
  
    > "Le autorizzazioni concesse all'utente 'XXXXXXXX\\&lt;nome utente&gt;' non sono sufficienti per eseguire questa operazione"  
  
7.  Accedere al portale Web con privilegi di amministratore, ad esempio, fare clic con il pulsante destro del mouse sull'icona di Internet Explorer e scegliere **Esegui come amministratore**.  
  
    Individuare l'URL del portale Web [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .   
    **Nota:** l'URL del *portale* è "Reports", non l'URL del *server* di report di "Reportserver".  Ad esempio   
    `https://<server name>/reports`(Indici per tabelle con ottimizzazione per la memoria).  
    `https://localhost/reports` funziona se la progettazione del report viene eseguita nel server di report.  
  
8.  Passare alla cartella che contiene il report. Il nome predefinito è *tutorial*, il nome del progetto o il nome digitato nel campo TargetReportFolder nelle proprietà del progetto.   
Fare clic sul nome del report **Sales Orders** per visualizzare il report visualizzabile nel browser.  
  
    ![ssrs_tutorial_tutorialfolder](../reporting-services/media/ssrs-tutorial-tutorialfolder.png)  
 
Questo passaggio conclude l'esercitazione relativa alla creazione di un report tabella semplice.  
  
## <a name="see-also"></a>Vedere anche  
[Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
  

