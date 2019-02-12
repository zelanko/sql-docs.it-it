---
title: 'Esercitazione: Creare un Report grafico rapido Offline (Generatore Report) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd22b4419b8300fdaf8db6e98a3eab9683fd226e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035542"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>Esercitazione: Creare un Report grafico rapido Offline (Generatore Report)
  In questa esercitazione verrà creato un grafico a torta utilizzando una procedura guidata e verranno quindi apportate alcune modifiche allo scopo di illustrare le potenzialità offerte all'utente. È possibile eseguire questa esercitazione in due modi diversi. Entrambi i metodi presentano stesso risultato: un grafico a torta simile a quello nell'illustrazione seguente:  
  
 ![Consente di visualizzare "Mio primo grafico a torta" in esecuzione](../media/rs-my1stpierunview.gif "My primo grafico a torta nella visualizzazione Esegui")  
  
## <a name="prerequisites"></a>Prerequisiti  
 Se si utilizzano dati XML o una query [!INCLUDE[tsql](../../../includes/tsql-md.md)], è necessario avere accesso a Generatore report di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. È possibile eseguire la versione autonoma o la versione ClickOnce disponibile in Gestione report o in un sito di SharePoint. Per le versioni ClickOnce, l'unica differenza riguarda il primo passaggio, ovvero l'apertura di Generatore report. Per altre informazioni, vedere [di installazione, disinstallazione e supporto di Generatore Report](../install-uninstall-and-report-builder-support.md).  
  
##  <a name="TwoWays"></a> Due modi per eseguire questa esercitazione  
  
-   [Creare il grafico a torta con dati XML](#CreatePieChartXML)  
  
-   [Creare il grafico a torta con una query Transact-SQL contenente dati](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>Utilizzo di dati XML per l'esercitazione  
 È possibile utilizzare dati XML copiandoli da questo argomento e incollandoli nella procedura guidata. Non è necessario essere connessi a un server di report o a un server di report in modalità integrata SharePoint e non è necessario accedere a un'istanza di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 [Creare il grafico a torta con dati XML](#CreatePieChartXML)  
  
### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>Utilizzo di una query Transact-SQL contenente dati per l'esercitazione  
 È possibile copiare una query contenente dati da questo argomento e incollarla nella procedura guidata. Sarà necessario disporre del nome di un'istanza di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e di credenziali sufficienti per l'accesso in sola lettura a qualsiasi database. Per la query del set di dati dell'esercitazione vengono utilizzati dati letterali, ma è necessario elaborare la query da un'istanza di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] per restituire i metadati richiesti per un set di dati del report.  
  
 Il vantaggio dell'utilizzo della query [!INCLUDE[tsql](../../../includes/tsql-md.md)] è dato dal fatto che in tutte le altre esercitazioni di Generatore report viene utilizzato lo stesso metodo, pertanto durante le altre esercitazioni si conosceranno già le azioni da effettuare.  
  
 Per la query [!INCLUDE[tsql](../../../includes/tsql-md.md)] sono necessari pochi altri prerequisiti. Per altre informazioni, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md).  
  
 [Creare il grafico a torta con una query Transact-SQL contenente dati](#CreatePieQueryData)  
  
## <a name="also-in-this-article"></a>Ulteriore contenuto dell'articolo  
 [Dopo aver eseguito la procedura guidata](#AfterWizard)  
  
 [Quali sono le novità](#WhatsNext)  
  
##  <a name="CreatePieChartXML"></a> Creazione del grafico a torta con dati XML  
  
#### <a name="to-create-the-pie-chart-with-xml-data"></a>Per creare il grafico a torta con dati XML  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** .  
  
    > [!NOTE]  
    >  Se il **Guida introduttiva** non viene visualizzato nella finestra di dialogo, dalle **Generatore Report** pulsante, fare clic su **New**.  
  
2.  Nel riquadro sinistro, verificare che **Report** sia selezionata.  
  
3.  Nel riquadro destro fare clic su **Creazione guidata grafico**, quindi scegliere **Crea**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dei dati** fare clic su **Nuova**.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
6.  È possibile assegnare qualsiasi nome a un'origine dati. Nella casella **Nome** digitare **Grafico a torta**.  
  
7.  Nel **Seleziona tipo di connessione** fare clic su **XML.**  
  
8.  Fare clic sulla scheda **Credenziali**, selezionare **Use current Windows user (Usa utente di Windows corrente). Potrebbe essere necessaria la delega Kerberos**, quindi fare clic su **OK**.  
  
9. Nella pagina **Scegliere una connessione a un'origine dei dati** fare clic su **Grafico a torta**, quindi su **Avanti**.  
  
10. Copiare il testo seguente e incollarlo nella casella grande al centro della **Progettazione query** pagina.  
  
    ```  
    <Query>  
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>  
    <XmlData>  
    <Root>  
    <S Sales="150">  
      <C FullName="Jae Pak" />  
    </S>  
    <S Sales="350">  
      <C FullName="Jillian  Carson" />  
    </S>  
    <S Sales="250">  
      <C FullName="Linda C Mitchell" />  
    </S>  
    <S Sales="500">  
      <C FullName="Michael Blythe" />  
    </S>  
    <S Sales="450">  
      <C FullName="Ranjit Varkey" />  
    </S>  
    </Root>  
    </XmlData>  
    </Query>  
    ```  
  
11. (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati su cui si baserà il grafico.  
  
12. Scegliere **Avanti**.  
  
13. Nella pagina **Scegliere un tipo di grafico** fare clic su **Torta**, quindi scegliere **Avanti**.  
  
14. Nella pagina relativa alla **disposizione dei campi del grafico** fare doppio clic sul campo **Vendite** nella casella **Campi disponibili**.  
  
     Il campo verrà spostato automaticamente nella casella **Valori** perché rappresenta un valore numerico.  
  
15. Trascinare il campo **FullName** dalla casella **Campi disponibili** alla casella **Categorie**. In alternativa è possibile fare doppio clic sul campo per spostarlo nella casella **Categorie**. Al termine fare clic su **Avanti**.  
  
16. Nel **scegliere uno stile** pagina **Oceano** è selezionata per impostazione predefinita. Fare clic sugli altri stili per visualizzarne l'aspetto.  
  
17. Scegliere **Fine**.  
  
     Osservare ora il nuovo report grafico a torta nell'area di progettazione. Gli elementi visualizzati sono esemplificativi. Nella legenda sono riportate le diciture Full Name 1, Full Name 2 e così via, anziché i nomi dei venditori, e le dimensioni delle sezioni della torta non sono precise. L'esempio serve solo per dare un'idea generale dell'aspetto del report.  
  
18. Per visualizzare il grafico a torta effettivo, fare clic su **Esegui** nella scheda **Home** della barra multifunzione.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)  
  
##  <a name="CreatePieQueryData"></a> Creazione del grafico a torta con una query [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
#### <a name="to-create-the-pie-chart-with-a-includetsqlincludestsql-mdmd-query-that-contains-data"></a>Per creare il grafico a torta con una query [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenente dati  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
2.  Nel **nuovo report o set di dati** finestra di dialogo, verificare che **Report** sia selezionata nel riquadro sinistro.  
  
3.  Nel riquadro destro fare clic su **Creazione guidata grafico**, quindi scegliere **Crea**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dei dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e scegliere **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati sui quali verrà basato il grafico.  
  
9. Scegliere **Avanti**.  
  
10. Nella pagina **Scegliere un tipo di grafico** fare clic su **Torta**, quindi scegliere **Avanti**.  
  
11. Nella pagina relativa alla **disposizione dei campi del grafico** fare doppio clic sul campo **Vendite** nella casella **Campi disponibili**.  
  
     Il campo verrà spostato automaticamente nella casella **Valori** perché rappresenta un valore numerico.  
  
12. Trascinare il campo **FullName** dalla casella **Campi disponibili** alla casella **Categorie**. In alternativa è possibile fare doppio clic sul campo per spostarlo nella casella **Categorie**. Al termine fare clic su **Avanti**.  
  
13. Per impostazione predefinita, nella pagina **Scegliere uno stile** è selezionato lo stile Oceano. Fare clic sugli altri stili per visualizzarne l'aspetto.  
  
14. Scegliere **Fine**.  
  
     Osservare ora il nuovo report grafico a torta nell'area di progettazione. Gli elementi visualizzati sono esemplificativi. Nella legenda sono riportate le diciture Full Name 1, Full Name 2 e così via, anziché i nomi dei venditori, e le dimensioni delle sezioni della torta non sono precise. L'esempio serve solo per dare un'idea generale dell'aspetto del report.  
  
15. Per visualizzare il grafico a torta effettivo, fare clic su **Esegui** nella scheda **Home** della barra multifunzione.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)  
  
##  <a name="AfterWizard"></a> Al termine della procedura guidata  
 Dopo aver terminato la creazione del report del grafico a torta, è possibile modificarlo nel modo desiderato. Nella scheda **Esegui** della barra multifunzione fare clic su **Progettazione**per continuare a modificarlo.  
  
### <a name="make-the-chart-bigger"></a>Ingrandire il grafico  
 Potrebbe essere necessario ingrandire il grafico a torta. Fare clic sul grafico, ma non sugli elementi in esso contenuti, per selezionarlo e trascinare l'angolo inferiore destro per ridimensionarlo.  
  
### <a name="add-a-report-title"></a>Aggiungere un titolo al report  
 Selezionare le parole **Titolo grafico** nella parte superiore del grafico, quindi digitare un titolo, ad esempio **Grafico a torta - Vendite**.  
  
### <a name="add-percentages"></a>Aggiungere percentuali  
  
##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Per visualizzare valori in percentuale come etichette in un grafico a torta  
  
1.  Fare clic sul grafico a torta e selezionare **Mostra etichette dati**. Le etichette dati dovrebbero apparire in ogni sezione del grafico a torta.  
  
2.  Fare clic su etichette e scegliere **proprietà etichetta serie**. Verrà visualizzata la finestra di dialogo **Proprietà etichetta serie** .  
  
3.  Tipo di `#PERCENT{P0}` per il **dati etichetta** opzione.  
  
     Il testo `{P0}` specifica la percentuale senza cifre decimali. Se si digita solo `#PERCENT`, i numeri avranno due cifre decimali. `#PERCENT` è una parola chiave che esegue un calcolo o una funzione. Ne sono disponibili anche diverse altre.  
  
 Per altre informazioni sulla personalizzazione di etichette e legende dei grafici, vedere [Visualizzare i valori in percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) e [Modificare il testo di un elemento legenda &#40;Generatore report e SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md).  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)  
  
##  <a name="WhatsNext"></a> Operazioni successive  
 Al termine della creazione del primo report in Generatore report, è possibile provare a eseguire le altre esercitazioni e iniziare a creare report basati su dati personalizzati. Per eseguire Generatore Report, è necessario disporre dell'autorizzazione per accedere alle origini dati, ad esempio database, con un *stringa di connessione*, che stabilisce l'effettiva connessione all'origine dati. L'amministratore di sistema disporrà di queste informazioni e potrà procedere alla configurazione.  
  
 Per eseguire le altre esercitazioni, è necessario disporre del nome di un'istanza di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e di credenziali sufficienti per l'accesso in sola lettura a qualsiasi database. L'amministratore di sistema potrà fornire i dati necessari.  
  
 Per salvare infine i report in un server di report o in un sito di SharePoint integrato con un server di report, è necessario disporre dell'URL e delle autorizzazioni appropriate. Tutti i report creati possono essere eseguiti direttamente dal computer, tuttavia quando vengono eseguiti dal server di report o dal sito di SharePoint i report offrono maggiori funzionalità. Per eseguire i propri report o quelli presenti sul server di report o nel sito di SharePoint in cui vengono pubblicati è necessario disporre delle autorizzazioni appropriate. Per ottenere l'accesso è necessario rivolgersi all'amministratore di sistema.  
  
 Prima di iniziare può essere utile leggere le informazioni su alcuni concetti e termini. Per altre informazioni, vedere [concetti di creazione di Report &#40;Generatore Report e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md). È inoltre consigliabile dedicarsi alla pianificazione prima di creare il primo report. Questa fase preliminare risulterà infatti molto utile. Per altre informazioni, vedere [pianificazione di un Report &#40;Generatore Report&#41;](../report-design/planning-a-report-report-builder.md).  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](../report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
