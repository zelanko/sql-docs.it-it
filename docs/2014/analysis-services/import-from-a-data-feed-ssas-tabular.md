---
title: Importare da un feed di dati (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb3a1cbcabc66492bbd780be4716ce69f15de37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080565"
---
# <a name="import-from-a-data-feed-ssas-tabular"></a>Importare da un feed di dati (SSAS tabulare)
  I feed di dati rappresentano uno o più flussi di dati XML generati da un'origine dati online e trasmessi a un documento o a un'applicazione di destinazione. È possibile importare dati da un feed di dati nel modello tramite l'Importazione guidata tabella.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Informazioni sull'importazione da un feed di dati](#prereq)  
  
-   [Importare dati da un set di dati di Azure DataMarket](#azure)  
  
-   [Importare feed di dati da origini dati pubbliche o aziendali](#importdata)  
  
-   [Importare feed di dati da elenchi SharePoint](#importlist)  
  
-   [Importare feed di dati da report Reporting Services](#importreport)  
  
##  <a name="prereq"></a>Informazioni sull'importazione da un feed di dati  
 È possibile importare dati in un modello tabulare dai tipi di feed di dati seguenti:  
  
 **Report Reporting Services**  
 È possibile utilizzare come origine dati in un modello un report di Reporting Services pubblicato in un sito di SharePoint o in un server di report. Quando si importano dati da un report di Reporting Services, è necessario specificare un file di definizione del report (con estensione rdl) come origine dati.  
  
 **Set di dati di Azure DataMarket**  
 Azure DataMarket è un servizio che fornisce un marketplace e un canale di recapito unici per informazioni quali i servizi cloud. Per i set di dati di Azure DataMarket è richiesta una chiave di account, anziché un account utente di Windows.  
  
 **Feed Atom**  
 Il feed deve essere un feed Atom. I feed RSS non sono supportati. Il feed deve essere disponibile pubblicamente oppure è necessario disporre dell'autorizzazione per connettersi ad esso con l'account di Windows con cui si è attualmente connessi.  
  
 I dati di un feed di dati vengono aggiunti una volta in un modello durante l'importazione. Per ottenere dati aggiornati dal feed, è possibile aggiornare i dati da Progettazione modelli o configurare una pianificazione dell'aggiornamento dei dati per il modello dopo la relativa distribuzione in un'istanza di produzione di Analysis Services. Per altre informazioni, vedere [Elaborare dati &#40;SSAS tabulare&#41;](process-data-ssas-tabular.md).  
  
##  <a name="azure"></a>Importare dati da un set di dati di Azure DataMarket  
 È possibile importare dati da un set di dati di Azure DataMarket, ad esempio una tabella del modello.  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>Per importare dati da un set di dati di Azure DataMarket  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**. Verrà visualizzata l'Importazione guidata tabella.  
  
2.  Nella pagina **Connessione a un'origine dati** , in **Feed di dati**, selezionare **Set di dati di Azure DataMarket**e quindi fare clic su **Avanti**.  
  
3.  Nella pagina **Connessione a un set di dati di Azure DataMarket** , in **Nome descrittivo**, digitare un nome descrittivo per il feed a cui si sta eseguendo l'accesso. Se si importano più feed o origini dati, l'utilizzo di nomi descrittivi per la connessione consente di ricordare come viene utilizzata la connessione.  
  
4.  In **URL feed di dati**digitare l'indirizzo per il feed di dati.  
  
5.  In **Impostazioni di sicurezza**, in **Chiave account**, digitare una chiave di account. Le chiavi di account vengono utilizzate da Analysis Services per accedere alle sottoscrizioni di DataMarket.  
  
6.  Fare clic su **Test connessione** per assicurarsi che il feed sia disponibile. In alternativa, è anche possibile fare clic su **Avanzate** per confermare che nell'URL di base o nell'URL del documento di servizio sia contenuto il documento di servizio o la query tramite cui viene fornito il feed.  
  
7.  Fare clic su **Avanti** per continuare con l'importazione.  
  
8.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando si aggiornano i dati e quindi fare clic su **Avanti**. Queste credenziali sono diverse dalla chiave di account.  
  
9. Nel campo **Nome descrittivo** della pagina **Selezione tabelle e viste** della procedura guidata digitare un nome descrittivo che consente di identificare la tabella in cui saranno inseriti tali dati dopo l'importazione  
  
10. Fare clic su **Visualizza anteprima e applica filtro** per rivedere i dati e modificare le selezioni di colonna. Non è possibile limitare le righe importate nel feed di dati del report ma è possibile rimuovere le colonne deselezionando le caselle di controllo. Fare clic su **OK**.  
  
11. Nella pagina **Selezione tabelle e viste** fare clic su **Fine**.  
  
##  <a name="importdata"></a>Importare feed di dati da origini dati pubbliche o aziendali  
 È possibile accedere a feed pubblici o compilare servizi dati personalizzati che consentono di generare feed Atom da sistemi di database proprietari o legacy.  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>Per importare dati da feed di dati pubblici o aziendali  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**. Verrà visualizzata l'Importazione guidata tabella.  
  
2.  Nella pagina **Connessione a un'origine dati** , in **Feed di dati**, selezionare **Altri feed**e quindi fare clic su **Avanti**.  
  
3.  Nella pagina **Connessione a un feed di dati** digitare un nome descrittivo per il feed a cui si sta eseguendo l'accesso. Se si importano più feed o origini dati, l'utilizzo di nomi descrittivi per la connessione consente di ricordare come viene utilizzata la connessione.  
  
4.  In **URL feed di dati**digitare l'indirizzo per il feed di dati. I valori validi sono i seguenti:  
  
    1.  Documento XML che contiene i dati Atom. Ad esempio, il seguente URL fa riferimento a un feed pubblico nel sito Web Open Government Data Initiative:  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  Documento con estensione atomsvc che specifica uno o più feed. Un documento con estensione atomsvc fa riferimento a un servizio o a un'applicazione che fornisce uno o più feed. Ogni feed viene specificato come query di base che restituisce il set dei risultati.  
  
         È possibile specificare un indirizzo URL a un documento con estensione atomsvc che risiede in un server Web o è possibile aprire il file da una cartella condivisa o locale nel computer. È possibile ottenere un documento con estensione atomsvc se ne è stato salvato uno nel computer durante l'esportazione di un report di Reporting Services oppure è possibile ottenere documenti con estensione atomsvc in una libreria di feed di dati creata per il sito di SharePoint.  
  
        > [!NOTE]  
        >  Si consiglia di specificare un documento con estensione atomsvc a cui è possibile accedere mediante un indirizzo URL o una cartella condivisa perché in questo modo è possibile configurare l'aggiornamento automatico dei dati per la cartella di lavoro in un secondo momento, dopo che questa è stata pubblicata in SharePoint. Il server può riutilizzare lo stesso indirizzo URL o la cartella di rete per aggiornare i dati se si specifica un percorso non locale nel computer.  
  
5.  Fare clic su **Test connessione** per assicurarsi che il feed sia disponibile. In alternativa, è anche possibile fare clic su **Avanzate** per confermare che nell'URL di base o nell'URL del documento di servizio sia contenuto il documento di servizio o la query tramite cui viene fornito il feed.  
  
6.  Fare clic su **Avanti** per continuare con l'importazione.  
  
7.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando si aggiornano i dati e quindi fare clic su **Avanti**.  
  
8.  Nel campo **Nome descrittivo** della pagina **Selezione tabelle e viste** della procedura guidata sostituire il contenuto del feed di dati con un nome descrittivo che consente di identificare la tabella in cui saranno contenuti tali dati dopo l'importazione  
  
9. Fare clic su **Visualizza anteprima e applica filtro** per rivedere i dati e modificare le selezioni di colonna. Non è possibile limitare le righe importate nel feed di dati del report ma è possibile rimuovere le colonne deselezionando le caselle di controllo. Fare clic su **OK**.  
  
10. Nella pagina **Selezione tabelle e viste** fare clic su **Fine**.  
  
##  <a name="importlist"></a>Importare feed di dati da elenchi SharePoint  
 È possibile importare un elenco SharePoint che dispone di un pulsante **Esporta come feed di dati** nella barra multifunzione di SharePoint. È possibile fare clic su questo pulsante per esportare l'elenco come feed.  
  
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>Per importare feed di dati da un elenco SharePoint  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**.  
  
2.  Nella pagina **Connessione a un'origine dati** , in **Feed di dati**, selezionare **Da altri feed di dati**e quindi fare clic su **Avanti**.  
  
3.  Nella pagina **Connessione a un feed di dati** digitare un nome descrittivo per il feed a cui si sta eseguendo l'accesso. Se si importano più feed o origini dati, l'utilizzo di nomi descrittivi per la connessione consente di ricordare come viene utilizzata la connessione.  
  
4.  In URL feed di dati digitare un indirizzo per il servizio dati elenco, sostituendo \<nome-server> con il nome effettivo del server SharePoint:  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  Fare clic su **Test connessione** per assicurarsi che il feed sia disponibile. In alternativa, è anche possibile fare clic su **Avanzate** per confermare che nell'URL del documento di servizio sia contenuto un indirizzo al servizio dati dell'elenco.  
  
6.  Fare clic su **Avanti** per continuare con l'importazione.  
  
7.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando si aggiornano i dati e quindi fare clic su **Avanti**.  
  
8.  Nella pagina **Seleziona tabelle e viste** della procedura guidata selezionare gli elenchi che si vogliono importare.  
  
    > [!NOTE]  
    >  È possibile importare solo elenchi contenenti colonne.  
  
9. Fare clic su **Visualizza anteprima e applica filtro** per rivedere i dati e modificare le selezioni di colonna. Non è possibile limitare le righe importate nel feed di dati del report ma è possibile rimuovere le colonne deselezionando le caselle di controllo. Fare clic su **OK**.  
  
10. Nella pagina **Selezione tabelle e viste** fare clic su **Fine**.  
  
##  <a name="importreport"></a>Importare feed di dati da report Reporting Services  
 Se si ha una distribuzione di [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Reporting Services, è possibile usare l'estensione per il rendering Atom per generare un feed di dati da un report esistente.  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>Per importare dati da un report pubblicato di Reporting Services  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**.  
  
2.  Nella pagina **Connessione a un'origine dati** , in **Feed di dati**, selezionare **Report**e quindi fare clic su **Avanti**.  
  
3.  In Nome descrittivo connessione della pagina Connessione a un report di Microsoft SQL Server Reporting Services digitare un nome descrittivo per il feed a cui si sta effettuando l'accesso. Se si importano più origini dati, l'utilizzo di nomi descrittivi per la connessione consente di ricordare come viene utilizzata la connessione.  
  
4.  Fare clic su **Sfoglia** e selezionare un server di report.  
  
     Se si usano normalmente i report in un server di report, è possibile che il server sia elencato in **Siti e server recenti**. In caso contrario, digitare in Nome l'indirizzo di un server di report e fare clic su **Apri** per esplorare le cartelle nel sito del server di report. Un indirizzo di esempio per un server di report potrebbe\<essere http://nomecomputer>/ReportServer.  
  
5.  Selezionare il report e fare clic su **Apri**. In alternativa, è possibile incollare un collegamento al report, compresi il percorso completo e il nome del report, nella casella di testo **Nome** . L'Importazione guidata tabella si connetterà al report e ne eseguirà il rendering nell'area di anteprima.  
  
     Se il report include parametri, per creare la connessione al report è necessario specificare un parametro. Quando si esegue questa operazione, nel feed di dati vengono importate solo le righe correlate al valore del parametro.  
  
    1.  Scegliere un parametro utilizzando la casella di riepilogo o la casella combinata fornita nel report.  
  
    2.  Fare clic su **Visualizza report** per aggiornare i dati.  
  
        > [!NOTE]  
        >  La visualizzazione del report salva i parametri selezionati insieme alla definizione del feed di dati.  
  
     Facoltativamente, fare clic su **Avanzate** per impostare proprietà specifiche del provider per il report.  
  
6.  Fare clic su **Test connessione** per assicurarsi che il report sia disponibile come feed di dati. In alternativa, è anche possibile fare clic su **Avanzate** per verificare che nella proprietà **Documento di servizio inline** sia contenuto il codice XML incorporato che consente di specificare la connessione al feed di dati.  
  
7.  Fare clic su **Avanti** per continuare con l'importazione.  
  
8.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando si aggiornano i dati e quindi fare clic su **Avanti**.  
  
9. Nella pagina **Selezione tabelle e viste** della procedura guidata selezionare la casella di controllo accanto alle parti di report che si vogliono importare come dati.  
  
     Alcuni report possono contenere più parti, inclusi tabelle, elenchi o grafici.  
  
10. Nella casella **Nome descrittivo** digitare il nome della tabella del modello in cui si vuole salvare il feed di dati.  
  
     Se non viene assegnato un nome, per impostazione predefinita verrà utilizzato il nome del controllo Reporting Services, ad esempio Tablix1, Tablix2. È consigliabile modificare questo nome durante l'importazione in modo da facilitare l'identificazione dell'origine del feed dei dati importato.  
  
11. Fare clic su **Visualizza anteprima e applica filtro** per rivedere i dati e modificare le selezioni di colonna. Non è possibile limitare le righe importate nel feed di dati del report ma è possibile rimuovere le colonne deselezionando le caselle di controllo. Fare clic su **OK**.  
  
12. Nella pagina **Selezione tabelle e viste** fare clic su **Fine**.  
  
## <a name="see-also"></a>Vedere anche  
 [Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [Tipi di dati supportati &#40;SSAS tabulare&#41;](tabular-models/data-types-supported-ssas-tabular.md)   
 [Rappresentazione &#40;SSAS tabulare&#41;](tabular-models/impersonation-ssas-tabular.md)   
 [Elaborare dati &#40;SSAS tabulare&#41;](process-data-ssas-tabular.md)   
 [Importare dati &#40;SSAS tabulare&#41;](import-data-ssas-tabular.md)  
  
  
