---
title: 'Esercitazione: Creare un report grafico rapido offline (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5cd666ec589737d83717e9b435a260bd2a0d0ef6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176895"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>Esercitazione: Creare un report grafico rapido offline (Generatore report)
  In questa esercitazione verrà creato un grafico a torta utilizzando una procedura guidata e verranno quindi apportate alcune modifiche allo scopo di illustrare le potenzialità offerte all'utente. È possibile eseguire questa esercitazione in due modi diversi. Entrambi i metodi hanno lo stesso risultato, ovvero un grafico a torta simile a quello illustrato nella figura seguente:

 !["Primo grafico a torta" nella visualizzazione Esegui](../media/rs-my1stpierunview.gif "Primo grafico a torta in Run View")

## <a name="prerequisites"></a>Prerequisites
 Se si utilizzano dati XML o una query [!INCLUDE[tsql](../../../includes/tsql-md.md)], è necessario avere accesso a Generatore report di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. È possibile eseguire la versione autonoma o la versione ClickOnce disponibile in Gestione report o in un sito di SharePoint. Per le versioni ClickOnce, l'unica differenza riguarda il primo passaggio, ovvero l'apertura di Generatore report. Per ulteriori informazioni, vedere [installazione, disinstallazione e supporto Generatore report](../install-uninstall-and-report-builder-support.md).

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
 [Dopo l'esecuzione della procedura guidata](#AfterWizard)

 [Passaggi successivi](#WhatsNext)

##  <a name="CreatePieChartXML"></a>Creazione del grafico a torta con dati XML

#### <a name="to-create-the-pie-chart-with-xml-data"></a>Per creare il grafico a torta con dati XML

1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.

     Verrà visualizzata la finestra di dialogo **Introduzione** .

    > [!NOTE]
    >  Se la finestra di dialogo **Introduzione** non viene visualizzata, dal pulsante **Generatore report** fare clic su **nuovo**.

2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **report** .

3.  Nel riquadro destro fare clic su **Creazione guidata grafico**, quindi scegliere **Crea**.

4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.

5.  Nella pagina **Scegliere una connessione a un'origine dei dati** fare clic su **Nuova**.

     Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .

6.  È possibile assegnare qualsiasi nome a un'origine dati. Nella casella **Nome** digitare **Grafico a torta**.

7.  Nella casella **Seleziona tipo di connessione** fare clic su **XML.**

8.  Fare clic sulla scheda **credenziali** , selezionare **USA utente di Windows corrente. Potrebbe essere richiesta la delega Kerberos**, quindi fare clic su **OK**.

9. Nella pagina **Scegliere una connessione a un'origine dei dati** fare clic su **Grafico a torta**, quindi su **Avanti**.

10. Copiare il testo seguente e incollarlo nella casella grande al centro della pagina **Progetta query** .

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

11. (Facoltativo) Fare clic sul pulsante Esegui ( **!** ) per visualizzare i dati su cui si baserà il grafico.

12. Fare clic su **Avanti**.

13. Nella pagina **Scegliere un tipo di grafico** fare clic su **Torta**, quindi scegliere **Avanti**.

14. Nella pagina relativa alla **disposizione dei campi del grafico** fare doppio clic sul campo **Vendite** nella casella **Campi disponibili**.

     Il campo verrà spostato automaticamente nella casella **Valori** perché rappresenta un valore numerico.

15. Trascinare il campo **FullName** dalla casella **Campi disponibili** alla casella **Categorie**. In alternativa è possibile fare doppio clic sul campo per spostarlo nella casella **Categorie**. Al termine fare clic su **Avanti**.

16. Per impostazione predefinita, nella pagina **Scegli uno stile** è selezionata l'opzione **oceano** . Fare clic sugli altri stili per visualizzarne l'aspetto.

17. Fare clic su **Fine**.

     Osservare ora il nuovo report grafico a torta nell'area di progettazione. Gli elementi visualizzati sono esemplificativi. Nella legenda sono riportate le diciture Full Name 1, Full Name 2 e così via, anziché i nomi dei venditori, e le dimensioni delle sezioni della torta non sono precise. L'esempio serve solo per dare un'idea generale dell'aspetto del report.

18. Per visualizzare il grafico a torta effettivo, fare clic su **Esegui** nella scheda **Home** della barra multifunzione.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)

##  <a name="CreatePieQueryData"></a>Creazione del grafico a torta con [!INCLUDE[tsql](../../../includes/tsql-md.md)] una query

#### <a name="to-create-the-pie-chart-with-a-tsql-query-that-contains-data"></a>Per creare il grafico a torta con una query [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenente dati

1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.

2.  Nella finestra di dialogo **nuovo report o set di dati** verificare che il **report** sia selezionato nel riquadro sinistro.

3.  Nel riquadro destro fare clic su **Creazione guidata grafico**, quindi scegliere **Crea**.

4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.

5.  Nella pagina **Scegliere una connessione a un'origine dei dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e scegliere **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.

    > [!NOTE]
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md).

6.  Nella pagina **Progetta query** fare clic su **modifica come testo**.

7.  Incollare la query seguente nel relativo riquadro:

    ```
    SELECT 150 AS Sales, 'Jae Pak' AS FullName 
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName 
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName 
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName 
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName 
    ```

8.  (Facoltativo) Fare clic sul pulsante Esegui ( **!** ) per visualizzare i dati su cui si baserà il grafico.

9. Fare clic su **Avanti**.

10. Nella pagina **Scegliere un tipo di grafico** fare clic su **Torta**, quindi scegliere **Avanti**.

11. Nella pagina relativa alla **disposizione dei campi del grafico** fare doppio clic sul campo **Vendite** nella casella **Campi disponibili**.

     Il campo verrà spostato automaticamente nella casella **Valori** perché rappresenta un valore numerico.

12. Trascinare il campo **FullName** dalla casella **Campi disponibili** alla casella **Categorie**. In alternativa è possibile fare doppio clic sul campo per spostarlo nella casella **Categorie**. Al termine fare clic su **Avanti**.

13. Per impostazione predefinita, nella pagina **Scegliere uno stile** è selezionato lo stile Oceano. Fare clic sugli altri stili per visualizzarne l'aspetto.

14. Fare clic su **Fine**.

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

1.  Fare clic con il pulsante destro del mouse sul grafico a torta e scegliere **Mostra etichette dati**. Le etichette dati dovrebbero apparire in ogni sezione del grafico a torta.

2.  Fare clic con il pulsante destro del mouse sulle etichette e scegliere **Proprietà etichetta serie**. Verrà visualizzata la finestra di dialogo **Proprietà etichetta serie** .

3.  Digitare `#PERCENT{P0}` per l'opzione **dati etichetta** .

     Il testo `{P0}` specifica la percentuale senza cifre decimali. Se si digita solo `#PERCENT`, i numeri avranno due cifre decimali. 
  `#PERCENT` è una parola chiave che esegue un calcolo o una funzione. Ne sono disponibili anche diverse altre.

 Per altre informazioni sulla personalizzazione di etichette e legende dei grafici, vedere [Visualizzare i valori in percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) e [Modificare il testo di un elemento legenda &#40;Generatore report e SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)

##  <a name="WhatsNext"></a>Passaggi successivi
 Al termine della creazione del primo report in Generatore report, è possibile provare a eseguire le altre esercitazioni e iniziare a creare report basati su dati personalizzati. Per eseguire Generatore report, è necessario disporre dell'autorizzazione per accedere alle origini dati, ad esempio i database, con una *stringa di connessione*che connette effettivamente all'origine dati. L'amministratore di sistema disporrà di queste informazioni e potrà procedere alla configurazione.

 Per eseguire le altre esercitazioni, è necessario disporre del nome di un'istanza di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e di credenziali sufficienti per l'accesso in sola lettura a qualsiasi database. L'amministratore di sistema potrà fornire i dati necessari.

 Per salvare infine i report in un server di report o in un sito di SharePoint integrato con un server di report, è necessario disporre dell'URL e delle autorizzazioni appropriate. Tutti i report creati possono essere eseguiti direttamente dal computer, tuttavia quando vengono eseguiti dal server di report o dal sito di SharePoint i report offrono maggiori funzionalità. Per eseguire i propri report o quelli presenti sul server di report o nel sito di SharePoint in cui vengono pubblicati è necessario disporre delle autorizzazioni appropriate. Per ottenere l'accesso è necessario rivolgersi all'amministratore di sistema.

 Prima di iniziare può essere utile leggere le informazioni su alcuni concetti e termini. Per ulteriori informazioni, vedere [concetti relativi alla creazione di Report &#40;Generatore report e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md). È inoltre consigliabile dedicarsi alla pianificazione prima di creare il primo report. Questa fase preliminare risulterà infatti molto utile. Per ulteriori informazioni, vedere [pianificazione di un Report &#40;Generatore report&#41;](../report-design/planning-a-report-report-builder.md).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#TwoWays)

## <a name="see-also"></a>Vedere anche
 [Esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md) [Generatore report in SQL Server 2014](report-builder-in-sql-server-2016.md)


