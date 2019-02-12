---
title: 'Lezione 6: Aggiunta di gruppi e totali (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bd3261a6669b1677fbfeff23b0017e622600007
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012742"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lezione 6: Aggiunta di gruppi e totali (Reporting Services)
  È possibile aggiungere gruppi e totali al report per organizzare e riepilogare i dati.  
  
 Per informazioni sull'aggiunta dei totali parziali ai report, vedere gli articoli in curah.microsoft.com: [Aggiunta di totali ai report di Reporting Services (SSRS)](https://go.microsoft.com/fwlink/p/?LinkId=403698).  
  
 **Contenuto dell'argomento:**  
  
-   [Per raggruppare i dati in un report](#bkmk_groupdata)  
  
-   [Per aggiungere totali a un report](#bkmk_addtotals)  
  
-   [Per aggiungere un totale giornaliero a un report](#bkmk_adddailytotal)  
  
-   [Per aggiungere un totale complessivo a un report](#bkmk_addgrandtotal)  
  
-   [Per pubblicare il Report nel Server di Report (facoltativo)](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> Per raggruppare i dati in un report  
  
1.  Fare clic sulla scheda **Progettazione** .  
  
2.  Se non viene visualizzato il **gruppi di righe** riquadro, fare doppio clic nell'area di progettazione e fare clic su **view** e quindi fare clic su **raggruppamento**.  
  
3.  Dal **i dati del Report** riquadro, trascinare il `Date` campo il **gruppi di righe** riquadro. Posizionarlo al di sopra della riga **(Dettagli)**.  
  
     L'handle di riga contiene ora una parentesi quadra per mostrare un gruppo. La tabella presenta ora due colonne Date, una su ogni lato di una linea verticale tratteggiata.  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  Dal **i dati del Report** riquadro, trascinare il `Order` campo il **gruppi di righe** riquadro. Posizionarlo al di sotto di Date e al di sopra di **(Dettagli)**.  
  
     L'handle di riga contiene ora due parentesi quadre per mostrare due gruppi. La tabella ora presenta due `Order` colonne, troppo.  
  
5.  Eliminare le colonne di data e l'ordine originale per il **a destra** della linea doppia. Verranno rimossi i singoli valori dei record in modo da visualizzare solo il valore del gruppo. Selezionare gli handle delle due colonne, fare clic con il pulsante destro del mouse e scegliere **Elimina colonne**.  
  
     ![Selezionare le colonne da eliminare](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "Selezionare colonne da eliminare")  
  
     È possibile formattare nuovamente le intestazioni di colonna e la data.  
  
6.  Per visualizzare un'anteprima del report, passare alla scheda **Anteprima** . Il risultato dovrebbe essere simile a quanto illustrato nella figura seguente:  
  
     ![Tabella raggruppata per data e quindi per numero di ordine](../../2014/tutorials/media/rs-basictablegroupspreview.gif "Tabella raggruppata per data e quindi per numero di ordine")  
  
##  <a name="bkmk_addtotals"></a> Per aggiungere totali a un report  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic con il pulsante destro del mouse sulla cella dell'area dati contenente il campo `[LineTotal]`e fare clic su **Aggiungi totale**.  
  
     Verrà aggiunta una riga con una somma degli importi di tutti gli ordini.  
  
3.  Fare clic con il pulsante destro del mouse sulla cella contenente il campo `[Qty]`e fare clic su **Aggiungi totale**.  
  
     Verrà aggiunta una somma delle quantità di tutti gli ordini alla riga dei totali.  
  
4.  Nella cella vuota a sinistra di `Sum[Qty]`digitare l'etichetta "**Order Total"**.  
  
5.  È possibile aggiungere un colore di sfondo alla riga dei totali. Selezionare le due celle della somma e la cella dell'etichetta.  
  
6.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Grigio chiaro**e scegliere **OK**.  
  
     ![Visualizzazione progettazione: Tabella di base con totale degli ordini](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "visualizzazione progettazione: Tabella di base con totale degli ordini")  
  
##  <a name="bkmk_adddailytotal"></a> Per aggiungere un totale giornaliero a un report  
  
1.  Fare doppio clic sulla cella Order, scegliere **Aggiungi totale**, fare clic su **dopo**.  
  
     Verrà aggiunta una nuova riga contenente somme delle quantità e degli importi di ogni giorno e l'etichetta "**totale**" nella colonna Order.  
  
2.  Digitare la parola **Daily** prima della parola **Total** nella stessa cella in modo da definire la frase **Daily Total**.  
  
3.  Selezionare la cella **Daily Total** , le due celle **Sum** e la cella vuota compresa tra di esse.  
  
4.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Arancione**e scegliere **OK**.  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> Per aggiungere un totale complessivo a un report  
  
1.  Fare clic con il pulsante destro del mouse sulla cella Date, scegliere **Aggiungi totale**e quindi fare clic su **Dopo**.  
  
     Verrà aggiunta una nuova riga che contiene le somme delle quantità e dollari per l'intero report e il **totale** etichettare il `Date` colonna.  
  
2.  Digitare la parola **Grand** prima della parola **Total** nella stessa cella in modo da definire la frase **Grand Total**.  
  
3.  Selezionare la cella **Grand Total** , le due celle **Sum** e le celle vuote comprese tra di esse.  
  
4.  Nel menu **Formato** selezionare **Colore di sfondo**, fare clic su **Azzurro**e scegliere **OK**.  
  
     ![Visualizzazione progettazione: Totale complessivo nella tabella di base](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "visualizzazione progettazione: Totale complessivo nella tabella di base")  
  
5.  Fare clic su Anteprima.  
  
     L'ultima pagina dovrebbe essere simile alla seguente:  
  
     ![Anteprima: Tabella di base con totale complessivo](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "Preview: Tabella di base con totale complessivo")  
  
##  <a name="bkmk_publishreport"></a> Per pubblicare il Report nel Server di Report (facoltativo)  
  
1.  Un passaggio facoltativo consiste nel pubblicare il report completato nel server di report in modalità nativa in modo che sia possibile visualizzare il report da Gestione report.  
  
2.  Sulla barra degli strumenti fare clic su **Progetto** , quindi scegliere **Proprietà tutorial**.  
  
3.  Nel **TargetServerURL** digitare il nome del nome del server di report, ad esempio **http://\<nomeserver > / reportserver**  
  
4.  Fare clic su **OK**.  
  
5.  Sulla barra degli strumenti fare clic su **Compila** , quindi scegliere **Distribuisci Tutorial**.  
  
     Se viene visualizzato un messaggio simile al seguente nella finestra di output, la distribuzione è stata completata correttamente.  
  
    > ------ Compilazione avviata - Progetto: tutorial, configurazione: Debug ------'Sales Orders.rdl' verrà ignorato. L'elemento è aggiornato. Compilazione completata -- 0 errori, 0 avvisi------ Inizio distribuzione: Progetto: tutorial, configurazione: Debug---distribuzione in http://\<nome server > / reportserverDeploying report '/ tutorial/Sales Orders'. Distribuzione completata-- 0 errori, 0 avvisi === compilazione: 1 completata o aggiornata, 0 non riuscite, 0 ignorate ==================== Distribuzione: 1 completata, 0 non riuscite, 0 ignorate ==========  
  
     Se viene visualizzato un messaggio di errore simile al seguente, verificare di disporre delle autorizzazione per il server di report e di aver avviato [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] con privilegi di amministratore.  
  
    > "Le autorizzazioni concesse all'utente ' XXXXXXXX\\< proprio nome utente\>' non sono sufficienti per eseguire questa operazione"  
  
6.  Avviare Gestione Report con privilegi di amministratore, ad esempio, fare doppio clic sull'icona per Internet Explorer e fare clic su **Esegui come amministratore**.  
  
     Selezionare l'URL Gestione report, ad esempio `http://<server name>/reports`.  
  
7.  Selezionare la cartella contenente il report e fare clic sul nome del report `Sales Orders` per visualizzare il report visualizzabile nel browser.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa alla creazione di un report tabella semplice.  
  
## <a name="see-also"></a>Vedere anche  
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
