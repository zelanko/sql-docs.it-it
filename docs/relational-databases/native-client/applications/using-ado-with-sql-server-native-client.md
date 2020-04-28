---
title: Uso di ADO
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 94c241e4dd089b0db667e5b24dbde541584bba41
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388262"
---
# <a name="using-ado-with-sql-server-native-client"></a>Utilizzo di ADO con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per sfruttare i vantaggi delle nuove funzionalità introdotte in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , ad esempio Mars (Multiple Active Result Set), notifiche delle query, tipi definiti dall'utente (UDT) o il nuovo tipo di dati **XML** , le applicazioni esistenti che utilizzano ActiveX Data Objects (ADO) utilizzano [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il provider OLE DB di Native client come provider di accesso ai dati.  
  
 L'uso del provider OLE DB di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client è necessario solo per utilizzare una delle caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se non si intende utilizzare tali caratteristiche, è possibile continuare a usare il provider di accesso ai dati corrente, generalmente SQLOLEDB. L'uso del provider OLE DB di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client è consigliabile se si intende potenziare un'applicazione esistente e si ha l'esigenza di utilizzare le nuove caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se si sviluppa una nuova applicazione, è consigliabile valutare l'opportunità di utilizzare ADO.NET e il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anziché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per accedere a tutte le nuove caratteristiche delle ultime versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sul provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], fare riferimento alla documentazione di .NET Framework SDK per ADO.NET.  
  
 Per consentire l'utilizzo in ADO delle nuove caratteristiche delle ultime versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sono stati apportati alcuni miglioramenti che estendono le caratteristiche principali di OLE DB. Questi miglioramenti consentono l'uso nelle applicazioni ADO delle più recenti funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e di due tipi di dati introdotti in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Consentono inoltre di sfruttare i miglioramenti ai tipi di dati **varchar**, **nvarchar** e **varbinary**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native client aggiunge la proprietà di inizializzazione SSPROP_INIT_DATATYPECOMPATIBILITY al set di proprietà DBPROPSET_SQLSERVERDBINIT per l'utilizzo da parte delle applicazioni ADO, in modo che i nuovi tipi di dati vengano esposti in modo compatibile con ADO. Inoltre, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client definisce anche una nuova parola chiave della stringa di connessione denominata **DataTypeCompatibility** impostata nella stringa di connessione.  
  
> [!NOTE]  
>  Le applicazioni ADO esistenti possono accedere a valori XML, UDT, nonché di campi binari e di testo valore di grandi dimensioni ed eseguirne l'aggiornamento utilizzando il provider SQLOLEDB. I nuovi tipi di dati **varchar(max)** , **nvarchar(max)** e **varbinary(max)** di grandi dimensioni vengono restituiti rispettivamente come i tipi ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary**. Le colonne XML vengono restituite come **adLongVarChar**, mentre le colonne con tipo definito dall'utente vengono restituite come **adVarBinary**. Tuttavia, se si utilizza il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client (SQLNCLI11) anziché SQLOLEDB, è necessario assicurarsi di impostare la parola chiave **DataTypeCompatibility** su "80" in modo che i nuovi tipi di dati vengano mappati correttamente ai tipi di dati ADO.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Abilitazione di SQL Server Native Client da ADO  
 Per abilitare l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client, le applicazioni ADO dovranno implementare le parole chiave seguenti nelle stringhe di connessione:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Per ulteriori informazioni sulle parole chiave delle stringhe di connessione ADO [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supportate in native client, vedere [utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Di seguito è riportato un esempio di creazione di una stringa di connessione ADO completamente abilitata per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] l'utilizzo con Native client, inclusa l'abilitazione della funzionalità Mars:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>Esempi  
 Nelle sezioni seguenti vengono forniti esempi di come è possibile utilizzare ADO con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il provider di OLE DB di Native Client.  
  
### <a name="retrieving-xml-column-data"></a>Recupero dei dati delle colonne XML  
 In questo esempio viene usato un recordset per recuperare e visualizzare i dati da una colonna XML nel database di esempio **AdventureWorks** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  
  
' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  
  
con.Close  
Set con = Nothing  
```  
  
> [!NOTE]  
>  L'applicazione di filtri al recordset non è supportata con le colonne XML. Se si prova ad applicare i filtri, viene generato un errore.  
  
### <a name="retrieving-udt-column-data"></a>Recupero dei dati delle colonne con tipo definito dall'utente  
 In questo esempio viene utilizzato un oggetto **Command** per eseguire una query SQL che restituisce un tipo definito dall'utente, vengono aggiornati i dati UDT, quindi i nuovi dati vengono nuovamente inseriti nel database. In questo esempio si presuppone che il tipo definito dall'utente (UDT) **Point** sia già stato registrato nel database.  
  
```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  
  
' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  
  
' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  
  
con.Close  
Set con = Nothing  
```  
  
### <a name="enabling-and-using-mars"></a>Abilitazione e utilizzo di MARS  
 In questo esempio, la stringa di connessione viene costruita per abilitare MARS tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il provider di OLE DB di Native client e quindi vengono creati due oggetti recordset da eseguire utilizzando la stessa connessione.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
  
Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  
  
Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  
  
con.Close  
Set con = Nothing  
```  
  
 Nelle versioni precedenti del provider OLE DB questo codice determinerebbe la creazione di una connessione implicita alla seconda esecuzione, in quanto per una sola connessione sarebbe possibile aprire un solo set attivo di risultati. Poiché la connessione implicita non sarebbe inserita nel pool di connessioni OLE DB, questa situazione provocherebbe overhead aggiuntivo. Con la funzionalità MARS esposta dal provider [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di OLE DB di Native client, si ottengono più risultati attivi in una connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
