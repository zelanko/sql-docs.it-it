---
title: Scrittura del codice di una gestione connessione personalizzata | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], coding
ms.assetid: b12b6778-1f01-4a7d-984d-73f2f7630aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e11738fb33c45bf1d18b32bb4e3b1be4d0cf6b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768914"
---
# <a name="coding-a-custom-connection-manager"></a>Scrittura del codice di una gestione connessione personalizzata
  Dopo avere creato una classe che eredita dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> e avere applicato l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> alla classe, è necessario eseguire l'override dell'implementazione delle proprietà e dei metodi della classe di base per fornire la funzionalità personalizzata.  
  
 Per esempi di gestioni connessione personalizzate, vedere [Sviluppo di un'interfaccia utente per una gestione connessione personalizzata](developing-a-user-interface-for-a-custom-connection-manager.md). Gli esempi di codice illustrati in questo argomento sono tratti dall'esempio di gestione connessione personalizzata SQL Server.  
  
> [!NOTE]  
>  La maggior parte delle attività, delle origini e delle destinazioni incluse in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] funziona solo con tipi specifici di gestioni connessioni predefinite. Questi esempi, pertanto, non possono essere testati con le attività e i componenti predefiniti.  
  
## <a name="configuring-the-connection-manager"></a>Configurazione della gestione connessione  
  
### <a name="setting-the-connectionstring-property"></a>Impostazione della proprietà ConnectionString  
 La proprietà <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> è un'importante proprietà ed è l'unica specifica di una gestione connessione personalizzata. La gestione connessione utilizza il valore di questa proprietà per connettersi all'origine dati esterna. Se si combinano diverse altre proprietà, ad esempio il nome del server e il nome del database, per creare la stringa di connessione, è possibile utilizzare una funzione di supporto per assemblare la stringa sostituendo determinati valori in un modello di stringa di connessione con il nuovo valore fornito dall'utente. Nell'esempio di codice seguente è illustrata un'implementazione della proprietà <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> che si basa su una funzione di supporto per assemblare la stringa.  
  
```vb  
' Default values.  
Private _serverName As String = "(local)"  
Private _databaseName As String = "AdventureWorks"  
Private _connectionString As String = String.Empty  
  
Private Const CONNECTIONSTRING_TEMPLATE As String = _  
  "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI"  
  
Public Property ServerName() As String  
  Get  
    Return _serverName  
  End Get  
  Set(ByVal value As String)  
    _serverName = value  
  End Set  
End Property  
  
Public Property DatabaseName() As String  
  Get  
    Return _databaseName  
  End Get  
  Set(ByVal value As String)  
    _databaseName = value  
  End Set  
End Property  
  
Public Overrides Property ConnectionString() As String  
  Get  
    UpdateConnectionString()  
    Return _connectionString  
  End Get  
  Set(ByVal value As String)  
    _connectionString = value  
  End Set  
End Property  
  
Private Sub UpdateConnectionString()  
  
  Dim temporaryString As String = CONNECTIONSTRING_TEMPLATE  
  
  If Not String.IsNullOrEmpty(_serverName) Then  
    temporaryString = temporaryString.Replace("<servername>", _serverName)  
  End If  
  If Not String.IsNullOrEmpty(_databaseName) Then  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName)  
  End If  
  
  _connectionString = temporaryString  
  
End Sub  
```  
  
```csharp  
// Default values.  
private string _serverName = "(local)";  
private string _databaseName = "AdventureWorks";  
private string _connectionString = String.Empty;  
  
private const string CONNECTIONSTRING_TEMPLATE = "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI";  
  
public string ServerName  
{  
  get  
  {  
    return _serverName;  
  }  
  set  
  {  
    _serverName = value;  
  }  
}  
  
public string DatabaseName  
{  
  get  
  {  
    return _databaseName;  
  }  
  set  
  {  
    _databaseName = value;  
  }  
}  
  
public override string ConnectionString  
{  
  get  
  {  
    UpdateConnectionString();  
    return _connectionString;  
  }  
  set  
  {  
    _connectionString = value;  
  }  
}  
  
private void UpdateConnectionString()  
{  
  
  string temporaryString = CONNECTIONSTRING_TEMPLATE;  
  
  if (!String.IsNullOrEmpty(_serverName))  
  {  
    temporaryString = temporaryString.Replace("<servername>", _serverName);  
  }  
  
  if (!String.IsNullOrEmpty(_databaseName))  
  {  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName);  
  }  
  
  _connectionString = temporaryString;  
  
}  
```  
  
### <a name="validating-the-connection-manager"></a>Convalida della gestione connessione  
 Eseguire l'override del metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> per verificare che la gestione connessione sia stata configurata correttamente e sia pronta per l'esecuzione. È necessario convalidare almeno il formato della stringa di connessione e verificare che siano stati forniti valori per tutti gli argomenti. L'esecuzione non può continuare finché la gestione connessione non restituisce <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> dal metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A>.  
  
 Nell'esempio di codice seguente è illustrata un'implementazione di <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> che verifica che l'utente abbia specificato un nome di server per la connessione.  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  If String.IsNullOrEmpty(_serverName) Then  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0)  
    Return DTSExecResult.Failure  
  Else  
    Return DTSExecResult.Success  
  End If  
  
End Function  
```  
  
```csharp  
public override Microsoft.SqlServer.Dts.Runtime.DTSExecResult Validate(Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  if (String.IsNullOrEmpty(_serverName))  
  {  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0);  
    return DTSExecResult.Failure;  
  }  
  else  
  {  
    return DTSExecResult.Success;  
  }  
  
}  
```  
  
### <a name="persisting-the-connection-manager"></a>Persistenza della gestione connessione  
 In genere non è necessario implementare la persistenza personalizzata per una gestione connessione. La persistenza personalizzata è richiesta solo quando le proprietà di un oggetto utilizzano tipi di dati complessi. Per altre informazioni, vedere [Sviluppo di oggetti personalizzati per Integration Services](../developing-custom-objects-for-integration-services.md).  
  
## <a name="working-with-the-external-data-source"></a>Utilizzo dell'origine dati esterna  
 I metodi più importanti di una gestione connessione personalizzata sono quelli che supportano la connessione a un'origine dati esterna. I metodi <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> vengono chiamati in vari momenti durante la fase di progettazione e la fase di esecuzione.  
  
### <a name="acquiring-the-connection"></a>Acquisizione della connessione  
 È necessario stabilire il tipo di oggetto appropriato che il metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> deve restituire dalla gestione connessione personalizzata. Ad esempio, una gestione connessione file restituisce solo una stringa che contiene un percorso e un nome file, mentre una gestione connessione ADO.NET restituisce un oggetto connessione gestito che già è aperto. Una gestione connessione OLE DB restituisce un oggetto connessione OLE DB nativo che non può essere utilizzato da codice gestito. La gestione connessione personalizzata SQL Server, da cui sono tratti i frammenti di codice in questo argomento, restituisce un oggetto `SqlConnection` aperto.  
  
 Gli utenti della gestione connessione devono sapere in anticipo quale tipo di oggetto aspettarsi, in modo che possano eseguire il cast dell'oggetto restituito nel tipo appropriato e accedere ai relativi metodi e proprietà.  
  
```vb  
Public Overrides Function AcquireConnection(ByVal txn As Object) As Object  
  
  Dim sqlConnection As New SqlConnection  
  
  UpdateConnectionString()  
  
  With sqlConnection  
    .ConnectionString = _connectionString  
    .Open()  
  End With  
  
  Return sqlConnection  
  
End Function  
```  
  
```csharp  
public override object AcquireConnection(object txn)  
{  
  
  SqlConnection sqlConnection = new SqlConnection();  
  
  UpdateConnectionString();  
  
  {  
    sqlConnection.ConnectionString = _connectionString;  
    sqlConnection.Open();  
  }  
  
  return sqlConnection;  
  
}  
```  
  
### <a name="releasing-the-connection"></a>Rilascio della connessione  
 L'azione eseguita nel metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> dipende dal tipo di oggetto restituito dal metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>. Se è disponibile un oggetto connessione aperto, è necessario chiuderlo e rilasciare le eventuali risorse che utilizza. Se <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> ha restituito solo un valore stringa, non è necessario eseguire alcuna azione.  
  
```vb  
Public Overrides Sub ReleaseConnection(ByVal connection As Object)  
  
  Dim sqlConnection As SqlConnection  
  
  sqlConnection = DirectCast(connection, SqlConnection)  
  
  If sqlConnection.State <> ConnectionState.Closed Then  
    sqlConnection.Close()  
  End If  
  
End Sub  
```  
  
```csharp  
public override void ReleaseConnection(object connection)  
{  
  SqlConnection sqlConnection;  
  sqlConnection = (SqlConnection)connection;  
  if (sqlConnection.State != ConnectionState.Closed)  
    sqlConnection.Close();  
}  
```  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una gestione connessione personalizzata](creating-a-custom-connection-manager.md)   
 [Sviluppo di un'interfaccia utente per una gestione connessione personalizzata](developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
