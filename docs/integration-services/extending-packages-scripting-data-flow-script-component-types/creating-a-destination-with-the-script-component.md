---
title: Creazione di una destinazione con il componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4a1fe05a5662dad7e674831c5e5b76b9c8c8263
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65801357"
---
# <a name="creating-a-destination-with-the-script-component"></a>Creazione di una destinazione con il componente script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare un componente di destinazione nel flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per salvare in un'origine dati i dati ricevuti dalle origini e dalle trasformazioni upstream. Normalmente, il componente di destinazione si connette all'origine dati tramite una gestione connessione esistente.  
  
 Per una panoramica sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Il componente script e il codice dell'infrastruttura che genera semplificano in modo significativo il processo di sviluppo di un componente del flusso di dati personalizzato. Tuttavia, per comprendere il funzionamento del componente script, può risultare utile leggere informazioni sui passaggi necessari per lo sviluppo di un componente del flusso di dati personalizzato nella sezione [Sviluppo di un componente del flusso di dati personalizzato](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), in particolare [Sviluppo di un componente di destinazione personalizzato](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Introduzione ai componenti di destinazione  
 Quando si aggiunge un componente script nella scheda Flusso di dati di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)], viene visualizzata la finestra di dialogo **Seleziona tipo componente script** in cui si richiede di selezionare uno script **Origine**, **Destinazione** o **Trasformazione**. In questa finestra di dialogo selezionare **Destinazione**.  
  
 Connettere quindi l'output di una trasformazione al componente di destinazione in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. A scopo di test, è possibile connettere direttamente un'origine a una destinazione senza alcuna trasformazione.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Configurazione di un componente di destinazione in modalità di progettazione metadati  
 Dopo aver selezionato l'opzione per creare un componente di destinazione, configurare il componente usando **Editor trasformazione Script**. Per altre informazioni, vedere [Configurazione del componente script nell'editor corrispondente](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Per selezionare il linguaggio di scripting che verrà usato dal componente script di destinazione, impostare la proprietà **ScriptLanguage** nella pagina **Script** della finestra di dialogo **Editor trasformazione Script**.  
  
> [!NOTE]  
>  Per impostare il linguaggio di scripting predefinito per il componente script, usare l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni**. Per ulteriori informazioni, vedere [General Page](../general-page-of-integration-services-designers-options.md).  
  
 Un componente di destinazione del flusso di dati include un input e nessun output. La configurazione dell'input per il componente è uno dei passaggi che vanno completati in modalità di progettazione metadati tramite **Editor trasformazione Script** prima di scrivere lo script personalizzato.  
  
### <a name="adding-connection-managers"></a>Aggiunta di gestioni connessioni  
 Normalmente, un componente di destinazione utilizza una gestione connessione esistente per connettersi all'origine dati in cui salva i dati dal flusso di dati. Nella pagina **Gestioni connessioni** di **Editor trasformazione Script** fare clic su **Aggiungi** per aggiungere la gestione connessione appropriata.  
  
 Tuttavia, una gestione connessione è solo un'unità pratica che incapsula e archivia le informazioni necessarie per la connessione a un'origine dati di un determinato tipo. È necessario scrivere codice personalizzato per caricare o salvare i dati e possibilmente per aprire e chiudere la connessione all'origine dati.  
  
 Per informazioni generali sull'uso delle gestioni connessioni con il componente Script, vedere [Connessione a origini dati nel componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Per altre informazioni sulla pagina **Gestioni connessioni** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Gestioni connessioni&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Configurazione di input e colonne di input  
 Un componente di destinazione include un input e nessun output.  
  
 Nella pagina **Colonne di input** di **Editor trasformazione Script** l'elenco di colonne contiene le colonne disponibili dell'output del componente a monte nel flusso di dati. Selezionare le colonne da salvare.  
  
 Per altre informazioni sulla pagina **Colonne di input** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Colonne di input&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
 La pagina **Input e output** di **Editor trasformazione Script** contiene un unico input, che è possibile rinominare. Si farà riferimento all'input in base al relativo nome nello script utilizzando la proprietà della funzione di accesso creata nel codice generato automaticamente.  
  
 Per altre informazioni sulla pagina **Input e output** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Input e output&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Aggiunta di variabili  
 Se si vuole usare variabili esistenti nello script, è possibile aggiungerle nei campi delle proprietà **ReadOnlyVariables** e **ReadWriteVariables** della pagina **Script** di **Editor trasformazione Script**.  
  
 Quando si aggiungono più variabili nei campi delle proprietà, separare i relativi nomi con virgole. È anche possibile selezionare più variabili facendo clic sul pulsante con i puntini di sospensione (**...**) accanto ai campi delle proprietà **ReadOnlyVariables** e **ReadWriteVariables** e selezionando le variabili nella finestra di dialogo **Seleziona variabili**.  
  
 Per informazioni generali sull'uso delle variabili con il componente script, vedere [Uso di variabili nel componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Per altre informazioni sulla pagina **Script** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Script&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Generazione di script per un componente di destinazione in modalità di progettazione codice  
 Dopo aver configurato i metadati per il componente, è possibile scrivere lo script personalizzato. Nella pagina **Script** di **Editor trasformazione Script** fare clic su **Modifica script** per aprire l'IDE di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), in cui è possibile aggiungere lo script personalizzato. Il linguaggio di scripting che si usa varia a seconda che sia stato selezionato [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# come linguaggio di scripting per la proprietà **ScriptLanguage** nella pagina **Script**.  
  
 Per importanti informazioni applicabili a tutti i tipi di componenti creati tramite il componente script, vedere [Codifica e debug del componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Informazioni sul codice generato automaticamente  
 Quando si apre l'IDE di VSTA dopo la creazione e la configurazione di un componente di destinazione, la classe modificabile **ScriptMain** viene visualizzata nell'editor del codice con uno stub per il metodo **ProcessInputRow**. La classe **ScriptMain** è quella in cui si scriverà il codice personalizzato, mentre **ProcessInputRow** è il metodo più importante in un componente di destinazione.  
  
 Se si apre la finestra **Esplora progetti** in VSTA, è possibile rilevare che il componente script ha generato anche gli elementi del progetto **BufferWrapper** e **ComponentWrapper** di sola lettura. La classe **ScriptMain** eredita dalla classe **UserComponent** nell'elemento di progetto **ComponentWrapper**.  
  
 In fase di esecuzione il motore flusso di dati chiama il metodo **ProcessInput** nella classe **UserComponent**, che esegue l'override del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> della classe padre <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. A sua volta il metodo **ProcessInput** esegue il ciclo delle righe nel buffer di input e chiama il metodo **ProcessInputRow** una volta per ogni riga.  
  
### <a name="writing-your-custom-code"></a>Scrittura di codice personalizzato  
 Per completare la creazione di un componente di destinazione personalizzato, è possibile creare script nei metodi seguenti disponibili nella classe **ScriptMain**.  
  
1.  Eseguire l'override del metodo **AcquireConnections** per connettersi all'origine dati esterna. Estrarre l'oggetto connessione o le informazioni di connessione necessarie dalla gestione connessione.  
  
2.  Eseguire l'override del metodo **PreExecute** per preparare il salvataggio dei dati. Ad esempio, è possibile creare e configurare un elemento **SqlCommand** e i relativi parametri in questo metodo.  
  
3.  Usare il metodo **ProcessInputRow** sottoposto a override per copiare ogni riga di input nell'origine dati esterna. Ad esempio, per una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile copiare i valori delle colonne nei parametri di un elemento **SqlCommand** ed eseguire il comando una volta per ogni riga. Per una destinazione file flat è possibile scrivere i valori per ogni colonna in un elemento **StreamWriter**, separandoli con il delimitatore di colonna.  
  
4.  Se necessario, eseguire l'override del metodo **PostExecute** per disconnettersi dall'origine dati esterna e per eseguire eventuali altre operazioni di pulizia richieste.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti visualizzano il codice necessario nella classe **ScriptMain** per creare un componente di destinazione.  
  
> [!NOTE]
>  Gli esempi usano la tabella **Person.Address** del database di esempio **AdventureWorks** e passano la prima e la quarta colonna, ovvero le colonne **int*AddressID*** e **nvarchar(30)City** attraverso il flusso di dati. Gli stessi dati vengono utilizzati negli esempi relativi a origine, trasformazione e destinazione in questa sezione. Per ogni esempio, sono documentati ulteriori prerequisiti e presupposti.  
  
### <a name="adonet-destination-example"></a>Esempio di destinazione ADO.NET  
 In questo esempio è illustrato un componente di destinazione che usa una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente per salvare i dati del flusso di dati in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se si desidera eseguire questo codice di esempio, è necessario configurare il pacchetto e il componente come segue:  
  
1.  Creare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] che usa il provider **SqlClient** per connettersi al database **AdventureWorks**.  
  
2.  Creare una tabella di destinazione eseguendo il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente nel database **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Aggiungere un nuovo componente script all'area di progettazione del flusso di dati e configurarlo come destinazione.  
  
4.  Connettere l'output di un'origine o di una trasformazione a monte al componente di destinazione in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. È possibile connettere direttamente un'origine a una destinazione senza alcuna trasformazione. Questo output deve specificare dati della tabella **Person.Address** del database di esempio **AdventureWorks** che contiene almeno le colonne **AddressID** e **City**.  
  
5.  Aprire l'**Editor trasformazione Script**. Nella pagina **Colonne di input** selezionare le colonne di input **AddressID** e **City**.  
  
6.  Nella pagina **Input e output** rinominare l'input con un nome più descrittivo, ad esempio **MyAddressInput**.  
  
7.  Nella pagina **Gestioni connessioni** aggiungere o creare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e specificare un nome, ad esempio **MyADONETConnectionManager**.  
  
8.  Nella pagina **Script** fare clic su **Modifica script** e immettere lo script seguente. Quindi, chiudere l'ambiente di sviluppo dello script.  
  
9. Chiudere **Editor trasformazione Script** ed eseguire l'esempio.  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>Esempio di destinazione file flat  
 In questo esempio è illustrato un componente di destinazione che utilizza una gestione connessione file flat esistente per salvare i dati del flusso di dati in un file flat.  
  
 Se si desidera eseguire questo codice di esempio, è necessario configurare il pacchetto e il componente come segue:  
  
1.  Creare una gestione connessione file flat che si connette a un file di destinazione. Il file non deve necessariamente esistere, in quanto verrà creato dal componente di destinazione. Configurare il file di destinazione come file delimitato da virgole che contiene le colonne **AddressID** e **City**.  
  
2.  Aggiungere un nuovo componente script all'area di progettazione del flusso di dati e configurarlo come destinazione.  
  
3.  Connettere l'output di un'origine o di una trasformazione a monte al componente di destinazione in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. È possibile connettere direttamente un'origine a una destinazione senza alcuna trasformazione. Questo output deve specificare i dati della tabella **Person.Address** del database di esempio **AdventureWorks** e deve contenere almeno le colonne **AddressID** e **City**.  
  
4.  Aprire l'**Editor trasformazione Script**. Nella pagina **Colonne di input** selezionare le colonne **AddressID** e **City**.  
  
5.  Nella pagina **Input e output** rinominare l'input con un nome più descrittivo, ad esempio **MyAddressInput**.  
  
6.  Nella pagina **Gestioni connessioni** aggiungere o creare la gestione connessione file flat usando un nome descrittivo, ad esempio **MyFlatFileDestConnectionManager**.  
  
7.  Nella pagina **Script** fare clic su **Modifica script** e immettere lo script seguente. Quindi, chiudere l'ambiente di sviluppo dello script.  
  
8.  Chiudere **Editor trasformazione Script** ed eseguire l'esempio.  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un'origine con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Sviluppo di un componente di destinazione personalizzato](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
