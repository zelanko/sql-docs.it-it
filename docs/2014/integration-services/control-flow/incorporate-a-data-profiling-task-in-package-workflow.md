---
title: Incorporare un'attività Profiling dati nel flusso di lavoro del pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d8096ee89a9c0b63c89849a02317dc23b2b130e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62831621"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>Incorporamento di un'attività Profiling dati nel flusso di lavoro del pacchetto
  Il profiling dati e la pulizia non sono attività potenziali per un processo automatizzato nelle fasi iniziali. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]l'output dell'attività Profiling dati richiede in genere l'analisi visiva e la valutazione umana per determinare se le violazioni segnalate sono significative o eccessive. Anche dopo il riconoscimento di problemi di qualità dei dati, è comunque necessario definire con attenzione un piano ben studiato per tentare di individuare l'approccio migliore per la pulizia.  
  
 Tuttavia, una volta stabiliti i criteri per la qualità dei dati, è possibile automatizzare operazioni periodiche di analisi e pulizia dell'origine dati. Considerare gli scenari seguenti:  
  
-   **Verifica della qualità dei dati prima di un caricamento incrementale**. Utilizzare l'attività Profiling dati per calcolare il profilo Rapporto di valori Null nella colonna dei nuovi dati destinati alla colonna CustomerName di una tabella Customers. Se la percentuale di valori Null è maggiore del 20%, inviare un messaggio di posta elettronica contenente l'output del profilo all'operatore e terminare il pacchetto. In caso contrario, continuare il caricamento incrementale.  
  
-   **Automazione della pulizia quando vengono soddisfatte le condizioni specificate**. Utilizzare l'attività Profiling dati per calcolare il profilo Inclusione valore della colonna State rispetto a una tabella di ricerca di stati e quello della colonna ZIP Code/Postal Code rispetto a una tabella di ricerca di CAP. Se l'attendibilità dell'inclusione dei valori di stato è minore dell'80%, ma quella dei valori di ZIP Code/Postal Code è maggiore del 99%, emergono due indicazioni. Innanzitutto, i dati relativi allo stato sono errati. In secondo luogo, i dati relativi a ZIP Code/Postal Code sono corretti. Avviare un'attività Flusso di dati per pulire i dati dello stato eseguendo una ricerca del valore dello stato corretto dal valore corrente di Zip Code/Postal Code.  
  
 Dopo aver ottenuto un flusso di lavoro in cui è possibile incorporare l'attività Flusso di dati, è necessario identificare i passaggi richiesti per aggiungere questa attività. Nella sezione seguente viene descritto il processo generale di incorporazione dell'attività Flusso di dati. Nelle due sezioni finali viene descritto come connettere l'attività Flusso di dati direttamente a un'origine dati o ai dati trasformati dal flusso di dati.  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>Definizione di un flusso di lavoro generale per l'attività Flusso di dati  
 Nella procedura seguente viene definito l'approccio generale per l'utilizzo dell'output dell'attività Profiling dati nel flusso di lavoro di un pacchetto.  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>Per utilizzare l'output dell'attività Profiling dati a livello di codice in un pacchetto  
  
1.  Aggiungere e configurare l'attività Profiling dati in un pacchetto.  
  
2.  Configurare le variabili del pacchetto che conterranno i valori che si desidera recuperare dai risultati del profilo.  
  
3.  Aggiungere e configurare un'attività Script. Connettere l'attività Script all'attività Profiling dati. Nell'attività Script scrivere codice che legge i valori desiderati dal file di output dell'attività Profiling dati e popola le variabili del pacchetto.  
  
4.  Nei vincoli di precedenza che connettono l'attività Script ai rami a valle nel flusso di lavoro, scrivere espressioni che utilizzano i valori delle variabili per indirizzare il flusso di lavoro.  
  
 Quando si incorpora l'attività Profiling dati nel flusso di lavoro di un pacchetto, tenere presenti queste due caratteristiche dell'attività:  
  
-   **Output dell'attività**. L'output dell'attività Profiling dati viene scritto in un file o in una variabile del pacchetto in formato XML in base allo schema DataProfile.xsd. Pertanto, è necessario eseguire una query sull'output XML se si desidera utilizzare i risultati del profilo nel flusso di lavoro condizionale di un pacchetto. A tale scopo, è possibile utilizzare il linguaggio di query Xpath. Per esaminare la struttura di questo output XML, è possibile aprire un file di output di esempio o lo schema stesso. Per aprire il file o lo schema di output, è [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]possibile utilizzare, un altro editor XML o un editor di testo, ad esempio Blocco note.  
  
    > [!NOTE]  
    >  Alcuni risultati del profilo visualizzati nel Visualizzatore profilo dati sono valori calcolati che non si trovano direttamente nell'output. Ad esempio, l'output del profilo Rapporto di valori Null nella colonna contiene il numero complessivo di righe e il numero di righe che contengono valori Null. È necessario eseguire una query su questi due valori, quindi calcolare la percentuale di righe che contengono valori Null per ottenere il rapporto di valori Null nella colonna.  
  
-   **Input dell'attività**. L'input dell'attività Profiling dati viene letto da tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Pertanto, è necessario salvare i dati presenti in memoria in tabelle di staging se si desidera eseguire il profiling di dati già caricati e trasformati nel flusso di dati.  
  
 Nelle sezioni seguenti questo flusso di lavoro generale viene applicato al profiling di dati provenienti direttamente da un'origine dati esterna o trasformati dall'attività Flusso di dati. Viene inoltre illustrato come gestire i requisiti di input e di output dell'attività Flusso di dati.  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>Connessione diretta dell'attività Profiling dati a un'origine dati esterna  
 L'attività Profiling dati consente di eseguire il profiling di dati provenienti direttamente da un'origine dati.  Per illustrare questa funzionalità, nell'esempio seguente viene utilizzata l'attività Profiling dati per calcolare un profilo Rapporto di valori Null nella colonna per le colonne della tabella Person.Address nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Viene quindi utilizzata un'attività Script per recuperare i risultati dal file di output e popolare le variabili del pacchetto che è possibile utilizzare per indirizzare il flusso di lavoro.  
  
> [!NOTE]  
>  Per questo semplice esempio è stata selezionata la colonna AddressLine2, in quanto contiene una percentuale elevata di valori Null.  
  
 L'esempio è costituito dai passaggi seguenti:  
  
-   Configurazione delle gestioni connessioni che eseguono la connessione all'origine dati esterna e al file di output che conterrà i risultati del profilo.  
  
-   Configurazione delle variabili del pacchetto che conterranno i valori necessari per l'attività Profiling dati.  
  
-   Configurazione dell'attività Profiling dati per calcolare il profilo Rapporto di valori Null nella colonna.  
  
-   Configurazione dell'attività Script per gestire l'output XML dell'attività Profiling dati.  
  
-   Configurazione dei vincoli di precedenza che controlleranno quali rami a valle nel flusso di lavoro vengono eseguiti in base ai risultati dell'attività Profiling dati.  
  
### <a name="configure-the-connection-managers"></a>Configurare le gestioni connessioni  
 Per questo esempio, sono disponibili due gestioni connessioni:  
  
-   Una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] che stabilisce la connessione al database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
-   Una gestione connessione file che crea il file di output che conterrà i risultati dell'attività Profiling dati.  
  
##### <a name="to-configure-the-connection-managers"></a>Per configurare le gestioni connessioni  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]creare un nuovo pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Aggiungere una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] al pacchetto. Configurare questa gestione connessione per l'uso del provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) e per la connessione a un'istanza disponibile del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     Per impostazione predefinita, il nome della gestione connessione è \<nome server>.AdventureWorks1.  
  
3.  Aggiungere una gestione connessione file al pacchetto. Configurare questa gestione connessione per la creazione del file di output per l'attività Profiling dati.  
  
     In questo esempio viene utilizzato il nome file DataProfile1.xml. Per impostazione predefinita, la gestione connessione e il file hanno lo stesso nome.  
  
### <a name="configure-the-package-variables"></a>Configurare le variabili del pacchetto  
 In questo esempio vengono utilizzate due variabili del pacchetto:  
  
-   La variabile ProfileConnectionName passa il nome della gestione connessione file all'attività Script.  
  
-   La variabile AddressLine2NullRatio passa il rapporto di valori Null calcolato per questa colonna dall'attività Script al pacchetto.  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>Per configurare le variabili del pacchetto che conterranno i risultati del profilo  
  
-   Nella finestra **Variabili** aggiungere e configurare le due variabili del pacchetto seguenti:  
  
    -   Immettere il nome, `ProfileConnectionName`, per una delle variabili e impostare il tipo di questa variabile su **String**.  
  
    -   Immettere il nome, `AddressLine2NullRatio`, per l'altra variabile e impostare il tipo di questa variabile su **Double**.  
  
### <a name="configure-the-data-profiling-task"></a>Configurare l'attività Profiling dati  
 L'attività Profiling dati deve essere configurata nel modo seguente:  
  
-   Per utilizzare come input i dati forniti dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .  
  
-   Per eseguire un profilo Rapporto di valori Null nella colonna sui dati di input.  
  
-   Per salvare i risultati del profilo nel file associato alla gestione connessione file.  
  
##### <a name="to-configure-the-data-profiling-task"></a>Per configurare l'attività Profiling dati  
  
1.  Aggiungere un'attività Profiling dati al flusso di controllo.  
  
2.  Aprire **Editor attività Profiling dati** per configurare l'attività.  
  
3.  Nella pagina **Generale** dell'editor, per **Destinazione**, selezionare il nome della gestione connessione file configurata in precedenza.  
  
4.  Nella pagina **Richieste profilo** dell'editor creare un nuovo profilo Rapporto di valori Null nella colonna.  
  
5.  Nel riquadro **Proprietà richiesta** , per **ConnectionManager**, selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] configurata in precedenza. Quindi, per **TableOrView**, selezionare Person.Address.  
  
6.  Chiudere l'editor attività Profiling dati.  
  
### <a name="configure-the-script-task"></a>Configurare l'attività Script  
 L'attività Script deve essere configurata per recuperare i risultati dal file di output e popolare le variabili del pacchetto configurate in precedenza.  
  
##### <a name="to-configure-the-script-task"></a>Per configurare l'attività Script  
  
1.  Aggiungere un'attività Script al flusso di controllo.  
  
2.  Connettere l'attività Script all'attività Profiling dati.  
  
3.  Aprire **Editor attività Script** per configurare l'attività.  
  
4.  Nella pagina **Script** selezionare il linguaggio di programmazione preferito. Quindi, rendere disponibili le due variabili del pacchetto per lo script:  
  
    1.  Per `ReadOnlyVariables`, selezionare `ProfileConnectionName`.  
  
    2.  Per **ReadWriteVariables**selezionare `AddressLine2NullRatio`.  
  
5.  Selezionare **Modifica script** per aprire l'ambiente di sviluppo dello script.  
  
6.  Aggiungere un riferimento allo spazio dei nomi System.Xml.  
  
7.  Immettere il codice di esempio che corrisponde al linguaggio di programmazione in uso:  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "https://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "https://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  Nel codice di esempio di questa procedura viene illustrato come caricare l'output dell'attività Profiling dati da un file. Per caricare invece l'output dell'attività Profiling dati da una variabile del pacchetto, vedere il codice di esempio alternativo riportato dopo questa procedura.  
  
8.  Chiudere l'ambiente di sviluppo dello script, quindi l'editor attività Script.  
  
#### <a name="alternative-code-reading-the-profile-output-from-a-variable"></a>Codice alternativo: lettura dell'output del profilo da una variabile  
 La procedura riportata in precedenza indica come caricare l'output dell'attività Profiling dati da un file. Un metodo alternativo consiste nel caricare questo output da una variabile del pacchetto. A tale scopo, è necessario apportare le modifiche seguenti al codice di esempio:  
  
-   Chiamare il metodo `LoadXml` della classe `XmlDocument` anziché il metodo `Load`.  
  
-   Nell'editor attività Script aggiungere il nome della variabile del pacchetto che contiene l'output del profilo all'elenco `ReadOnlyVariables` dell'attività.  
  
-   Passare il valore stringa della variabile al metodo `LoadXML` come illustrato nell'esempio di codice seguente. In questo esempio viene utilizzato "ProfileOutput" come nome della variabile del pacchetto che contiene l'output del profilo.  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>Configurare i vincoli di precedenza  
 I vincoli di precedenza devono essere configurati per controllare quali rami a valle nel flusso di lavoro vengono eseguiti in base ai risultati dell'attività Profiling dati.  
  
##### <a name="to-configure-the-precedence-constraints"></a>Per configurare i vincoli di precedenza  
  
-   Nei vincoli di precedenza che connettono l'attività Script ai rami a valle nel flusso di lavoro, scrivere espressioni che utilizzano i valori delle variabili per indirizzare il flusso di lavoro.  
  
     Ad esempio, è possibile impostare **Operazione valutazione** del vincolo di precedenza su **Espressione e vincolo**. È quindi possibile utilizzare `@AddressLine2NullRatio < .90` come valore dell'espressione. In questo modo il flusso di lavoro segue il percorso selezionato quando le attività precedenti vengono completate e quando la percentuale di valori Null nella colonna selezionata è minore del 90%.  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>Connessione dell'attività Profiling dati ai dati trasformati dal flusso di dati  
 Anziché direttamente da un'origine dati, è possibile eseguire il profiling dei dati che sono già stati caricati e trasformanti nel flusso di lavoro. L'attività Profiling dati funziona, tuttavia, solo per dati persistenti, non per dati in memoria. Pertanto, è necessario utilizzare dapprima un componente di destinazione per salvare i dati trasformati in una tabella di staging.  
  
> [!NOTE]  
>  Quando si configura l'attività Profiling dati, è necessario selezionare tabelle e colonne esistenti. Pertanto, è necessario creare la tabella di staging in fase di progettazione prima di poter configurare l'attività. In altri termini, questo scenario non consente l'utilizzo di una tabella temporanea creata in fase di esecuzione.  
  
 Dopo aver salvato i dati in una tabella di staging, è possibile effettuare le azioni seguenti:  
  
-   Utilizzare l'attività Profiling dati per eseguire il profiling dei dati.  
  
-   Utilizzare un'attività Script per leggere i risultati come descritto in precedenza in questo argomento.  
  
-   Utilizzare questi risultati per indirizzare il flusso di lavoro successivo del pacchetto.  
  
 Nella procedura seguente viene fornito l'approccio generale per l'utilizzo dell'attività Profiling dati per eseguire il profiling di dati trasformati dal flusso di dati. Molti passaggi sono simili a quelli descritti in precedenza per il profiling dei dati provenienti direttamente da un'origine dati esterna. Può essere necessario rivedere questi passaggi precedenti per ulteriori informazioni su come configurare i vari componenti.  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>Per utilizzare l'attività Profiling dati nel flusso di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]creare un pacchetto.  
  
2.  Nel flusso di dati aggiungere, configurare e connettere le origini e le trasformazioni appropriate.  
  
3.  Nel flusso di dati aggiungere, configurare e connettere un componente di destinazione che salva i dati trasformati in una tabella di staging.  
  
4.  Nel flusso di controllo aggiungere e configurare un'attività Profiling dati che calcola i profili desiderati rispetto ai dati trasformati nella tabella di staging. Connettere l'attività Profiling dati all'attività Flusso di dati.  
  
5.  Configurare le variabili del pacchetto che conterranno i valori che si desidera recuperare dai risultati del profilo.  
  
6.  Aggiungere e configurare un'attività Script. Connettere l'attività Script all'attività Profiling dati. Nell'attività Script scrivere codice che legge i valori desiderati dall'output dell'attività Profiling dati e popola le variabili del pacchetto.  
  
7.  Nei vincoli di precedenza che connettono l'attività Script ai rami a valle nel flusso di lavoro, scrivere espressioni che utilizzano i valori delle variabili per indirizzare il flusso di lavoro.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione dell'attività Profiling dati](data-profiling-task.md)   
 [Visualizzatore profilo dati](data-profile-viewer.md)  
  
  
