---
title: Usare espressioni di proprietà nei pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- dynamic properties
- updating package properties
- SSIS packages, expressions
- expressions [Integration Services], property expressions
- property expressions [Integration Services]
ms.assetid: a4bfc925-3ef6-431e-b1dd-7e0023d3a92d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a926405f2c35ff62b3589003ebe015fe920b743
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176421"
---
# <a name="use-property-expressions-in-packages"></a>utilizzo delle espressioni di proprietà nei pacchetti
  Un'espressione di proprietà è un'espressione assegnata a una proprietà per consentire l'aggiornamento dinamico della proprietà in fase di esecuzione. Un'espressione di proprietà, ad esempio, consente di aggiornare la riga A utilizzata dall'attività Invia messaggi inserendo un indirizzo di posta elettronica archiviato in una variabile.

 È possibile aggiungere un'espressione a pacchetti, attività, cicli Foreach, cicli For, sequenze, enumeratori Foreach, gestori eventi, gestioni connessioni a livello di pacchetto o progetto oppure provider di log. Qualsiasi proprietà di questi oggetti che sia di lettura/scrittura può implementare un'espressione di proprietà. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] supporta l'utilizzo delle espressioni di proprietà in alcune proprietà personalizzate di componenti del flusso di dati. Le variabili e i vincoli di precedenza non supportano le espressioni di proprietà, ma includono speciali proprietà in cui è possibile utilizzare espressioni.

 Le espressioni di proprietà possono essere aggiornate in modi diversi:

-   È possibile includere variabili definite dall'utente nelle configurazioni di pacchetto e aggiornarle quindi in fase di distribuzione del pacchetto. In fase di esecuzione l'espressione di proprietà viene valutata in base al valore aggiornato della variabile.

-   Le variabili di sistema incluse in espressioni vengono aggiornate in fase di esecuzione. Il risultato della valutazione della proprietà è pertanto diverso.

-   Le funzioni di data e ora, che vengono valutate in fase di esecuzione, passano i valori aggiornati alle espressioni di proprietà.

-   Le variabili incluse in espressioni possono essere aggiornate tramite gli script eseguiti dall'attività Script e dal componente Script.

 Le espressioni vengono compilate in base al linguaggio delle espressioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]. Nelle espressioni è possibile includere variabili definite dall'utente o di sistema, insieme agli operatori, alle funzioni e ai cast di tipo del linguaggio delle espressioni.

> [!NOTE]
>  I nomi delle variabili di sistema e delle variabili definite dall'utente devono essere specificati rispettando la distinzione tra maiuscole e minuscole.

 Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md).

 Un utilizzo importante delle espressioni di proprietà è la personalizzazione delle configurazioni per ogni istanza di pacchetto distribuita. Ciò consente l'aggiornamento dinamico delle proprietà del pacchetto in ambienti diversi. È possibile, ad esempio, creare un'espressione di proprietà che assegna una variabile alla stringa di connessione di una gestione connessione e aggiorna quindi la variabile in fase di distribuzione del pacchetto in modo da garantire la validità della stringa di connessione in fase di esecuzione. Le configurazioni di pacchetto vengono caricate prima della valutazione delle espressioni di proprietà.

 Una proprietà può utilizzare una sola espressione di proprietà e a sua volta un'espressione di proprietà può essere applicata a una sola proprietà. È tuttavia possibile compilare più espressioni di proprietà identiche e assegnarle a proprietà diverse.

 Alcune proprietà vengono impostate utilizzando valori specificati da enumeratori. Per fare riferimento a un membro di un enumeratore in un'espressione di proprietà, è necessario utilizzare il valore numerico equivalente al nome descrittivo di tale membro dell'enumeratore. Se ad esempio un'espressione di proprietà imposta la proprietà `LoggingMode` in cui viene utilizzato un valore dell'enumerazione `DTSLoggingMode`, l'espressione di proprietà dovrà utilizzare 0, 1 o 2, anziché i nomi descrittivi `Enabled`, `Disabled` o `UseParentSetting`. Per altre informazioni, vedere [Costanti enumerate in espressioni di proprietà](enumerated-constants-in-property-expressions.md).

## <a name="property-expression-user-interface"></a>Interfaccia utente delle espressioni di proprietà
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] offre un set di strumenti per la compilazione e la gestione delle espressioni di proprietà.

-   Pagina **Espressioni** degli editor personalizzati delle attività e dei contenitori Ciclo For e Ciclo Foreach. In pagina **Espressioni** è possibile modificare espressioni e visualizzare un elenco delle espressioni di proprietà usate da un'attività o da un contenitore Ciclo Foreach o Ciclo For.

-   Finestra **Proprietà** per la modifica di espressioni e la visualizzazione di un elenco delle espressioni di proprietà usate da un pacchetto o dagli oggetti di pacchetto.

-   Finestra di dialogo **Editor espressioni di proprietà** per la creazione, l'aggiornamento e l'eliminazione di espressioni di proprietà.

-   Finestra di dialogo **Generatore di espressioni** per la compilazione di espressioni tramite strumenti grafici. In finestra di dialogo **Generatore di espressioni** le espressioni possono venire valutate senza assegnare il risultato alla proprietà in modo da consentirne prima la revisione.

 Nella figura seguente si illustrano i componenti dell'interfaccia utente che consentono di aggiungere, modificare e rimuovere espressioni di proprietà.

 ![Interfaccia utente per espressioni di proprietà](../media/ssis-propertyexpressionui.gif "Interfaccia utente per espressioni di proprietà")

 Nella finestra **Proprietà** e nella pagina **Espressioni** fare clic sul pulsante Sfoglia **(...)** al livello della raccolta **Espressioni** per aprire la finestra di dialogo **Editor espressioni di proprietà**. Nella finestra Editor espressioni di proprietà è possibile eseguire il mapping una proprietà a un'espressione e digitare espressioni di proprietà. Se per creare e convalidare l'espressione si vogliono usare gli strumenti grafici, fare clic sul pulsante Sfoglia **(...)** al livello dell'espressione per aprire la finestra di dialogo **Generatore di espressioni**, quindi creare o modificare e facoltativamente convalidare l'espressione.

 È possibile accedere alla finestra di dialogo **Generatore di espressioni** anche dalla finestra di dialogo **Editor espressioni di proprietà** .

#### <a name="to-work-with-property-expressions"></a>Per utilizzare le espressioni di proprietà

-   [Aggiungere o modificare un'espressione di proprietà](add-or-change-a-property-expression.md)

### <a name="setting-property-expressions-of-data-flow-components"></a>Impostazione di espressioni di proprietà per i componenti dei flussi di dati
 Se si crea un pacchetto in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], le proprietà dei componenti di un flusso di dati che supportano espressioni di proprietà vengono esposte sull'attività Flusso di dati a cui appartengono. Per aggiungere, modificare e rimuovere le espressioni di proprietà dei componenti di un flusso di dati, è necessario fare clic con il pulsante destro del mouse sull'attività Flusso di dati a cui appartengono tali componenti e scegliere **Proprietà**. Nella finestra Proprietà sono elencate le proprietà dei componenti del flusso di dati per le quali è possibile utilizzare espressioni di proprietà. Per creare o modificare un'espressione di proprietà per la proprietà SamplingValue di una trasformazione Campionamento righe in un flusso di dati di nome SampleCustomer, ad esempio, fare clic con il pulsante destro del mouse sull'attività Flusso di dati a cui appartiene la trasformazione Campionamento righe e scegliere **Proprietà**. La proprietà SamplingValue è elencata nella finestra Proprietà, con il formato [SampleCustomer].[SamplingValue].

 Nella finestra Proprietà è possibile aggiungere, modificare e rimuovere espressioni di proprietà per i componenti dei flussi di dati come avviene per le espressioni di proprietà degli altri tipi di oggetti di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . La finestra Proprietà consente inoltre di accedere alle altre finestre di dialogo e agli altri generatori necessari per aggiungere, modificare o rimuovere espressioni di proprietà per i componenti dei flussi di dati. Per altre informazioni sulle proprietà dei componenti dei flussi di dati che è possibile aggiornare tramite espressioni di proprietà, vedere [Proprietà personalizzate delle trasformazioni](../data-flow/transformations/transformation-custom-properties.md).

## <a name="loading-property-expressions"></a>Caricamento di espressioni di proprietà
 Non è possibile specificare o controllare il momento in cui avviene il caricamento delle espressioni di proprietà. Le espressioni di proprietà vengono valutate e caricate al momento della convalida del pacchetto e degli oggetti di pacchetto. La convalida avviene quando si salva il pacchetto, quando si apre il pacchetto in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] e quando si esegue il pacchetto.

 I valori aggiornati delle proprietà degli oggetti di pacchetto che utilizzano espressioni di proprietà non saranno pertanto disponibili in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] finché il pacchetto non verrà salvato, eseguito o riaperto dopo l'aggiunta delle espressioni di proprietà.

 Anche le espressioni di proprietà associate ad altri tipi di oggetti, quali gestioni connessioni, provider di log ed enumeratori, vengono caricate al momento della chiamata di metodi specifici del tipo di oggetto. Le proprietà delle gestioni connessioni, ad esempio, vengono caricate prima della creazione di un'istanza della connessione da parte di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .

 Le espressioni di proprietà vengono caricate dopo il caricamento delle configurazioni di pacchetto. Le variabili, ad esempio, vengono innanzitutto aggiornate dalle relative configurazioni e quindi vengono valutate e caricate le espressioni di proprietà che utilizzano tali variabili. Di conseguenza, le espressioni di proprietà utilizzano sempre i valori delle variabili impostati dalle configurazioni.

> [!NOTE]
>  Non è possibile usare `Set` l'opzione dell'utilità **dtexec** per popolare un'espressione di proprietà.

 Nella tabella seguente è indicato quando vengono valutate e caricate le espressioni di proprietà di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .

|Tipo oggetto|Caricamento e valutazione|
|-----------------|-----------------------|
|Pacchetto, ciclo Foreach, ciclo For, sequenza, attività e componenti dei flussi di dati|Dopo il caricamento delle configurazioni<br /><br /> Prima della convalida<br /><br /> Prima dell'esecuzione|
|Gestioni connessioni|Dopo il caricamento delle configurazioni<br /><br /> Prima della convalida<br /><br /> Prima dell'esecuzione<br /><br /> Prima della creazione di un'istanza della connessione|
|Provider di log|Dopo il caricamento delle configurazioni<br /><br /> Prima della convalida<br /><br /> Prima dell'esecuzione<br /><br /> Prima dell'apertura dei log|
|Enumeratori Foreach|Dopo il caricamento delle configurazioni<br /><br /> Prima della convalida<br /><br /> Prima dell'esecuzione<br /><br /> Prima di ogni enumerazione del ciclo|

## <a name="using-property-expressions-in-the-foreach-loop"></a>Utilizzo di espressioni di proprietà nel ciclo Foreach
 È spesso consigliabile implementare un'espressione di proprietà per impostare il valore della proprietà `ConnectionString` delle gestioni connessioni utilizzate nel contenitore Ciclo Foreach. Dopo che l'enumeratore esegue il mapping tra il relativo valore corrente e una variabile in ogni iterazione del ciclo, l'espressione di proprietà può usare il valore di questa variabile per aggiornare dinamicamente il valore della proprietà `ConnectionString`.

 Se si desidera utilizzare espressioni di proprietà con la proprietà `ConnectionString` delle gestioni connessioni per file, più file, file flat e più file flat utilizzate da un ciclo Foreach, sarà necessario tenere conto di alcuni aspetti. Un pacchetto può essere configurato in modo da eseguire contemporaneamente più file eseguibili impostando la proprietà `MaxConcurrentExecutables` su un valore maggiore di 1 o al valore -1. Il valore -1 indica che il numero massimo di file eseguibili che possono essere eseguiti contemporaneamente è uguale al numero di processori più due. Per evitare conseguenze negative dell'esecuzione parallela di file eseguibili, il valore di `MaxConcurrentExecutables` deve essere impostato su 1. Se la proprietà `MaxConcurrentExecutables` non è impostata su 1, il valore della proprietà `ConnectionString` non può essere garantito e i risultati sono imprevedibili.

 Considerare, ad esempio, un ciclo Foreach che enumera i file in una cartella, recupera i nomi dei file e quindi utilizza l'attività Esegui SQL per inserire ogni nome di file in una tabella. Se la proprietà `MaxConcurrentExecutables` non è impostata su 1 e due istanze dell'attività Esegui SQL tentano di scrivere contemporaneamente nella tabella, potrebbero verificarsi conflitti di scrittura.

## <a name="sample-property-expressions"></a>Espressioni di proprietà di esempio
 Le espressioni di esempio seguenti illustrano l'utilizzo di variabili di sistema, operatori, funzioni e valori letterali stringa nelle espressioni di proprietà.

### <a name="property-expression-for-the-loggingmode-property-of-a-package"></a>Espressione di proprietà per la proprietà LoggingMode di un pacchetto
 L'espressione di proprietà seguente consente di impostare la proprietà LoggingMode di un pacchetto. Nell'espressione sono utilizzate le funzioni DAY e GETDATE per ottenere un valore intero che rappresenta la parte del giorno in una data. Se il numero del giorno è 1 o 15, la registrazione verrà abilitata, altrimenti sarà disabilitata. Il valore 1 è l'intero equivalente del membro `Enabled`dell'enumeratore LoggingMode e il valore 2 è l'intero equivalente del membro. `Disabled` Nell'espressione è necessario utilizzare il valore numerico corrispondente al nome del membro desiderato dell'enumeratore.

 `DAY((DT_DBTIMESTAMP)GETDATE())==1||DAY((DT_DBTIMESTAMP)GETDATE())==15?1:2`

### <a name="property-expression-for-the-subject-of-an-e-mail-message"></a>Espressione di proprietà per la riga Oggetto di un messaggio di posta elettronica
 L'espressione di proprietà seguente consente di impostare la proprietà Subject dell'attività Invia messaggi e di inserire un testo appropriato nel messaggio di posta elettronica. Nell'espressione vengono utilizzati valori letterali stringa, variabili di sistema, l'operatore di concatenazione (+), l'operatore cast e le funzioni DATEDIFF e GETDATE. Le variabili di sistema sono `PackageName` e `StartTime` .

 `"PExpression-->Package: (" + @[System::PackageName] + ") Started:"+  (DT_WSTR, 30) @[System::StartTime] + " Duration:"  +  (DT_WSTR,10) (DATEDIFF( "ss", @[System::StartTime] , GETDATE()  )) + " seconds"`

 Se il nome del pacchetto è EmailRowCountPP, eseguito il 3/4/2005, con durata di esecuzione di 9 secondi, l'espressione viene valutata nella stringa seguente.

 PExpression-->Package: (EmailRowCountPP) Started:3/4/2005 11:06:18 AM Duration:9 seconds.

### <a name="property-expression-for-the-message-of-an-e-mail-message"></a>Espressione di proprietà per il testo di un messaggio di posta elettronica
 L'espressione di proprietà seguente consente di impostare la proprietà MessageSource dell'attività Invia messaggi. Nell'espressione vengono utilizzati valori letterali stringa, variabili definite dall'utente e l'operatore di concatenazione (+). Le variabili definite dall'utente sono denominate `nasdaqrawrows`, `nyserawrows`e `amexrawrows`. La stringa "\n" indica un ritorno a capo.

 `"Rows Processed: "  +   "\n" +"   NASDAQ: "  +   (dt_wstr,9)@[nasdaqrawrows]   + "\n" + "   NYSE: "  +  (dt_wstr,9)@[nyserawrows]  + "\n" + "   Amex: "  +  (dt_wstr,9)@[amexrawrows]`

 Se `nasdaqrawrows` è 7058, `nyserawrows` è 3528 e `amexrawrows` è 1102, l'espressione restituisce la stringa seguente.

 Rows Processed:

 NASDAQ: 7058

 NYSE: 3528

 AMEX: 1102

### <a name="property-expression-for-the-executable-property-of-an-execute-process-task"></a>Espressione di proprietà per la proprietà Executable dell'attività Esegui processo
 L'espressione di proprietà seguente consente di impostare la proprietà Executable dell'attività Esegui processo. Nell'espressione viene utilizzata una combinazione di valori letterali stringa, operatori e funzioni, e precisamente le funzioni DATEPART e GETDATE e l'operatore condizionale.

 `DATEPART("weekday", GETDATE()) ==2?"notepad.exe":"mspaint.exe"`

 Se la data odierna corrisponde al secondo giorno della settimana, l'attività Esegui processo esegue notepad.exe. In caso contrario esegue mspaint.exe.

### <a name="property-expression-for-the-connectionstring-property-of-a-flat-file-connection-manager"></a>Espressione di proprietà per la proprietà ConnectionString di una gestione connessione file flat
 L'espressione di proprietà seguente consente di impostare la proprietà ConnectionString di una gestione connessione file flat. Nell'espressione viene utilizzata una sola variabile definita dall'utente, ovvero la variabile `myfilenamefull`, che specifica il percorso di un file di testo.

 `@[User::myfilenamefull]`

> [!NOTE]
>  È possibile accedere alle espressioni di proprietà per le gestioni connessioni solo tramite la finestra Proprietà. Per visualizzare le proprietà di una gestione connessione, è necessario selezionare la gestione connessione nella sezione **Gestioni connessioni** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , quando la finestra Proprietà è aperta, oppure fare clic con il pulsante destro del mouse sulla gestione connessione e scegliere **Proprietà**.

### <a name="property-expression-for-the-configstring-property-of-a-text-file-log-provider"></a>Espressione di proprietà per la proprietà ConfigString di un provider di log File di testo
 L'espressione di proprietà seguente consente di impostare la proprietà ConfigString di un provider di log File di testo. Nell'espressione viene usata una sola variabile definita dall'utente, ovvero la variabile `varConfigString`, che contiene il nome della gestione connessione file da utilizzare. La gestione connessione file specifica il percorso del file di testo in cui verranno scritte le voci di log.

 `@[User::varConfigString]`

> [!NOTE]
>  È possibile accedere alle espressioni di proprietà per i provider di log solo tramite la finestra Proprietà. Per visualizzare le proprietà di un provider di log, è necessario selezionare il provider di log nella scheda **Esplora pacchetti** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , quando la finestra Proprietà è aperta, oppure fare clic con il pulsante destro del mouse sul provider log in Esplora pacchetti e scegliere **Proprietà**.

## <a name="external-resources"></a>Risorse esterne

-   [Espressione e Highlighter di configurazione (Progetto CodePlex)](https://go.microsoft.com/fwlink/?LinkId=146625)

-   Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com

## <a name="see-also"></a>Vedere anche
 [Uso di variabili nei pacchetti](../use-variables-in-packages.md)


