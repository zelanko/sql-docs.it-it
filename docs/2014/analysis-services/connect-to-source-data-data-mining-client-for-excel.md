---
title: Connettersi ai dati di origine (Client di Data Mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
ms.assetid: 548672ce-e403-4aca-b67a-c2c797f053dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 468686314bb2446415a6883c6233708f9cbd1d2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087096"
---
# <a name="connect-to-source-data-data-mining-client-for-excel"></a>Connessione ai dati di origine (client di data mining per Excel)
  In questo argomento viene descritto come creare e utilizzare le connessioni utilizzate per archiviare i modelli di data mining e per accedere a dati esterni archiviati in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Connessioni di data mining.** La connessione iniziale creata all'avvio dei componenti aggiuntivi viene utilizzata per accedere agli algoritmi, analizzare i dati e archiviare la struttura e i modelli di data mining.  
  
 La connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è necessaria per utilizzare gli strumenti di modellazione e di visualizzazione dei componenti aggiuntivi perché questi ultimi dipendono da strutture dei dati e algoritmi forniti da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Connessioni alle origini dati esterne.** È inoltre possibile creare connessioni a dati esterni durante la compilazione di modelli o il salvataggio dei risultati. È ad esempio possibile creare un modello di data mining in un server, quindi eseguire una query di stima sul modello utilizzando i dati archiviati in un'altra istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], in una tabella dati di Excel o in un'origine dati esterna, ad esempio [!INCLUDE[msCoName](../includes/msconame-md.md)] Access. Ogni volta che si accede a una nuova origine dati, viene chiesto di creare una connessione tramite una finestra di dialogo.  
  
##  <a name="bkmk_prereq2"></a> Prerequisiti  
 Per questa versione dei componenti aggiuntivi è necessario che l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sia SQL Server 2012. Se si desidera connettersi a una versione precedente di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è disponibile una versione separata dei componenti aggiuntivi. Esistono versioni dei componenti aggiuntivi che supportano SQL Server 2005, SQL Server 2008 e SQL Server 2008 R2.  
  
 Per connettersi a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è necessario disporre delle autorizzazioni per accedere al server di database. È necessario inoltre che le sessioni di data mining siano abilitate e che l'utente disponga delle autorizzazioni di lettura o lettura/scrittura per gli oggetti di database archiviati nel server.  
  
##  <a name="bkmk_connect"></a> Creazione di connessioni al Server Data Mining  
 Il **connessioni** gruppo nel Client di Data Mining per Excel e strumenti di analisi tabelle per Excel sono disponibili strumenti per la gestione delle connessioni a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   È possibile creare la connessione durante l'installazione del componente aggiuntivo o aggiungere una connessione in un secondo momento.  
  
-   È possibile creare più connessioni e modificare le connessioni in qualsiasi momento, a meno che non sia in corso la creazione o l'esecuzione di query su un modello.  
  
     Non cambiare o chiudere una connessione durante l'elaborazione di un modello di data mining. Potrebbero infatti verificarsi perdite di dati del modello di data mining oppure il modello potrebbe diventare inutilizzabile.  
  
-   Solo una connessione può essere attiva in un determinato momento.  
  
### <a name="connections-in-the-excel-add-ins"></a>Connessioni nei componenti aggiuntivi per Excel  
 Il **connessioni** gruppo nel Client di Data Mining per Excel e strumenti di analisi tabelle per Excel è possibile gestire le connessioni a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
##### <a name="create-a-new-server-connection-in-the-excel-add-ins"></a>Creazione di una nuova connessione al server nei componenti aggiuntivi per Excel  
  
1.  Fare clic sul **connessione** pulsante il **Analizza** oppure **Data Mining** della barra multifunzione.  
  
    > [!NOTE]  
    >  Il testo del pulsante indica se è presente una connessione. Quando nel foglio di lavoro non è stata stabilita alcuna connessione, il pulsante contiene il testo "\<Nessuna connessione >." Se invece nel foglio di lavoro è stata precedentemente effettuata una connessione, nel pulsante verrà visualizzato il nome della connessione.  
  
2.  Nel **connessioni ad Analysis Services** finestra di dialogo, fare clic su **New**.  
  
3.  Nel **nuova connessione Analysis Services** finestra di dialogo, digitare il nome del server.  
  
4.  Specificare il metodo di autenticazione.  
  
5.  Selezionare un database di **nome del catalogo** elenco a discesa. Se non esiste un database nell'istanza, selezionare **(impostazione predefinita)** .  
  
6.  Digitare un nome descrittivo per la connessione.  
  
7.  Fare clic su **Test connessione** per verificare che il server e il database siano disponibili.  
  
8.  Fare clic su **OK**, quindi su **Chiudi**.  
  
### <a name="connections-using-a-web-service"></a>Connessioni tramite un servizio Web  
 Se si utilizza un'architettura thin client per consentire l'esplorazione di cubi e dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è inoltre possibile configurare una connessione a un server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tramite servizi Web. Per informazioni sulla definizione di un client basato sul Web, vedere la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Se si dispone dell'accesso a un server configurato per i servizi Web, sarà possibile specificare il tipo di connessione al momento della creazione della connessione.  
  
##### <a name="create-an-http-connection-to-analysis-services"></a>Creazione di una connessione HTTP ad Analysis Services  
  
1.  Aprire il **nuova connessione Analysis Services** nella finestra di dialogo.  
  
2.  Come nome del server digitare http:// seguito dall'URL assegnato al server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Digitare il nome utente e la password necessari per accedere al servizio Web.  
  
### <a name="connections-in-the-visio-add-in"></a>Connessioni nel componente aggiuntivo per Visio  
 A differenza di Excel, in Visio non è disponibile una barra multifunzione degli strumenti e non sono presenti pulsanti specifici per la creazione o il monitoraggio delle connessioni. La connessione dati viene invece creata quando si seleziona una forma di data mining e la si rilascia in una pagina di Visio. Nella procedura guidata verrà chiesto di selezionare il modello per la forma e di impostare altre opzioni.  
  
 Se in precedenza sono state utilizzate connessioni a un'origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in Excel, tali connessioni vengono elencate come possibili origini dati da selezionare.  
  
##### <a name="create-a-connection-for-a-visio-shape"></a>Creazione di una connessione per una forma di Visio  
  
1.  Aprire il modello di data mining e selezionare una delle forme di data mining.  
  
2.  Trascinare e rilasciare la forma in una pagina vuota.  
  
3.  Nel **Vybrat zdroj** finestra di dialogo, selezionare una data di origine dall'elenco oppure fare clic su **New**.  
  
4.  Se si seleziona **New**, seguire la procedura descritta in precedenza per specificare un nome di catalogo e il server o per la connessione tramite un servizio Web.  
  
##  <a name="bkmk_change"></a> Se si cambia connessione  
 È possibile creare più connessioni nello stesso foglio di lavoro, ma può essere attiva solo una connessione alla volta. Viene visualizzato il nome della connessione corrente nel **connessione** pulsante.  
  
 Nel Client di Data Mining per Excel, è anche possibile verificare la stringa di connessione e lo stato per la connessione corrente facendo **traccia** e quindi scegliendo **connessione corrente**.  
  
#### <a name="use-a-different-server-connection"></a>Utilizzo di una connessione a un altro server  
  
1.  Fare clic su **connessione**.  
  
2.  Nel **connessioni ad Analysis Services** riquadro, selezionare una connessione di **altre connessioni** elenco e fare clic su **Make Current**.  
  
3.  Fare clic su **Test connessione** per verificare che sia disponibile la connessione.  
  
 Al termine dell'elaborazione di un modello di data mining, i risultati vengono archiviati localmente e se si interrompe la connessione a un server per connettersi a un altro server non si hanno ripercussioni sui dati. È consigliabile tuttavia evitare di cambiare connessione o di interrompere la connessione durante l'elaborazione di un modello di data mining, in quanto si potrebbero danneggiare i dati.  
  
#### <a name="modify-an-existing-server-connection"></a>Modifica di una connessione al server esistente  
  
1.  Non è possibile modificare una connessione esistente; se si desidera connettersi a un database o a un server diverso, è necessario creare una nuova connessione.  
  
2.  Se è necessario modificare la stringa di connessione per aumentare il timeout per le query o aggiungere altri parametri specifici dell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], un'opzione consiste nel modificare il file DMC, in cui è archiviata la stringa di connessione.  
  
     \<unità: > \Users\\< myusername\>\AppData\Local\Microsoft\Data componente aggiuntivo Data Mining  
  
##  <a name="bkmk_extconnections"></a> La connessione alle origini dati esterne  
 Mentre gli strumenti disponibili nel **Analyze** sulla barra multifunzione funzionano esclusivamente con i dati in Excel, gli strumenti disponibili nel **Data Mining** della barra multifunzione consentono di connettersi direttamente alle origini dati esterne da utilizzare come input per il modello o per campionamento.  
  
 Gli strumenti seguenti in questi componenti aggiuntivi supportano l'utilizzo di dati esterni per il data mining:  
  
-   [Dati di esempio &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md)  
  
-   [Procedura guidata classificazione &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Procedura guidata stima &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Creazione guidata del cluster &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Procedura guidata previsione &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Crea struttura di Data Mining &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
-   [Grafico di accuratezza &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
-   [Grafico profitti &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
  
-   [Matrice di classificazione &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
### <a name="using-analysis-services-as-a-data-source"></a>Utilizzo di Analysis Services come origine dati  
 Non è possibile accedere direttamente ai dati archiviati in un modello tabulare o in un cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. In alternativa, è possibile creare una connessione in Excel al server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e utilizzare i dati per creare un modello.  
  
### <a name="relational-data-sources"></a>Origini dati relazionali  
 Se si desidera utilizzare i dati da un'origine relazionale come input al modello, è possibile connettersi alle seguenti versioni di SQL Server:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
 È inoltre possibile ottenere dati da qualsiasi altra origine dati relazionale supportata come origine dati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per informazioni sulle origini dati supportate, vedere [origini dati nei modelli multidimensionali](multidimensional-models/data-sources-in-multidimensional-models.md)  
  
 Si noti che i seguenti tipi di dati non possono essere utilizzati per il data mining e si verificherà un errore se vengono inclusi quando si compila un modello:  
  
-   ntext  
  
-   BINARY  
  
## <a name="see-also"></a>Vedere anche  
 [Traccia &#40;Client di Data Mining per Excel&#41;](trace-data-mining-client-for-excel.md)  
  
  
