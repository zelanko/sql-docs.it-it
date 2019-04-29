---
title: Il recupero dei dati di tipo definito dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085b1783214e7f629f1cb91084303edacd151c25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874638"
---
# <a name="retrieving-udt-data"></a>Recupero di dati UDT
  Per creare un tipo definito dall'utente (UDT) nel client, l'assembly registrato come tipo definito dall'utente in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere disponibile per l'applicazione client. L'assembly UDT può essere posizionato nella stessa directory dell'applicazione oppure nella Global Assembly Cache (GAC). È inoltre possibile impostare un riferimento all'assembly nel progetto.  
  
## <a name="requirements-for-using-udts-in-adonet"></a>Requisiti per l'utilizzo di tipi definiti dall'utente in ADO.NET  
 Per consentire la creazione del tipo definito dall'utente sul client, è necessario che l'assembly caricato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'assembly sul client siano compatibili. Per i tipi definiti dall'utente con il formato di serializzazione `Native`, gli assembly devono essere strutturalmente compatibili. Gli assembly definiti con il formato `UserDefined` devono essere disponibili sul client.  
  
 Per recuperare i dati non elaborati da una colonna con tipo definito dall'utente in una tabella, non è necessario che sul client sia disponibile una copia dell'assembly UDT.  
  
> [!NOTE]  
>  **SqlClient** potrebbe non riuscire a caricare un tipo definito dall'utente in caso di versioni non corrispondenti di tipo definito dall'utente o altri problemi. In questo caso, utilizzare i normali meccanismi per la risoluzione di problemi per determinare il motivo per cui l'assembly in cui è contenuto il tipo definito dall'utente non viene individuato dall'applicazione chiamante. Per ulteriori informazioni, consultare l'argomento intitolato "Diagnostica degli errori tramite gli assistenti al debug gestito" nella documentazione di .NET Framework.  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>Accesso ai tipi definiti dall'utente con un oggetto SqlDataReader  
 È possibile utilizzare un oggetto `System.Data.SqlClient.SqlDataReader` dal codice client per recuperare un set di risultati in cui è contenuta una colonna con tipo definito dall'utente, esposta come un'istanza dell'oggetto.  
  
### <a name="example"></a>Esempio  
 In questo esempio viene mostrato come utilizzare il metodo `Main` per creare un nuovo oggetto `SqlDataReader`. All'interno del codice di esempio si verificano le azioni seguenti:  
  
1.  Il metodo Main crea un nuovo oggetto `SqlDataReader` e recupera i valori della tabella Points contenente una colonna con tipo definito dall'utente denominata Point.  
  
2.  Il tipo definito dall'utente di Point espone le coordinate X e Y definite come numeri interi.  
  
3.  Il tipo definito dall'utente definisce un metodo `Distance` e un metodo `GetDistanceFromXY`.  
  
4.  Il codice di esempio recupera i valori delle colonne con tipo definito dall'utente di chiave primaria per dimostrare le funzionalità del tipo definito dall'utente.  
  
5.  Il codice di esempio chiama i metodi `Point.Distance` e `Point.GetDistanceFromXY`.  
  
6.  I risultati vengono visualizzati nella finestra della console.  
  
> [!NOTE]  
>  Nell'applicazione deve essere già presente un riferimento all'assembly UDT.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>Associazione di tipi definiti dall'utente come byte  
 In alcune situazioni può risultare utile recuperare i dati non elaborati dalla colonna con tipo definito dall'utente. Può accadere che il tipo non sia disponibile localmente o non si desideri creare un'istanza del tipo definito dall'utente. È possibile leggere i byte non elaborati in una matrice di byte utilizzando il **GetBytes** metodo di un `SqlDataReader`. Tale metodo legge un flusso di byte dall'offset di colonna specificato nel buffer di una matrice, a partire dall'offset del buffer specificato. Un'altra opzione consiste nell'usare uno dei **GetSqlBytes** oppure **GetSqlBinary** metodi e leggere tutto il contenuto in un'unica operazione. In entrambi i casi non viene mai creata un'istanza dell'oggetto UDT, pertanto non è necessario impostare un riferimento al tipo definito dall'utente nell'assembly client.  
  
### <a name="example"></a>Esempio  
 In questo esempio mostra come recuperare il **punto** i dati come byte non elaborati in una matrice di byte utilizzando un `SqlDataReader`. Il codice utilizza un oggetto `System.Text.StringBuilder` per convertire i byte non elaborati in una rappresentazione di stringa da visualizzare nella finestra della console.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>Esempio di utilizzo di GetSqlBytes  
 In questo esempio mostra come recuperare il **punto** i dati come byte non elaborati in una singola operazione utilizzando il **GetSqlBytes** (metodo). Il codice utilizza un oggetto `StringBuilder` per convertire i byte non elaborati in una rappresentazione di stringa da visualizzare nella finestra della console.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>Utilizzo dei parametri UDT  
 I tipi definiti dall'utente possono essere utilizzati come parametri sia di input che di output nel codice ADO.NET.  
  
## <a name="using-udts-in-query-parameters"></a>Utilizzo dei tipi definiti dall'utente nei parametri di query  
 I tipi definiti dall'utente possono essere utilizzati come valori di parametro in caso di configurazione di un oggetto `SqlParameter` per un oggetto `System.Data.SqlClient.SqlCommand`. L'enumerazione `SqlDbType.Udt` di un oggetto `SqlParameter` viene utilizzata per indicare che il parametro è un tipo definito dall'utente durante la chiamata al metodo `Add` nella raccolta `Parameters`. Il `UdtTypeName` proprietà di un `SqlCommand` oggetto viene usato per specificare il nome completo del tipo in questione nel database utilizzando il *object_name* sintassi. Anche se non è richiesto, l'utilizzo che il nome completo, elimina l'ambiguità dal codice.  
  
> [!NOTE]  
>  Una copia locale dell'assembly UDT deve essere disponibile per il progetto client.  
  
### <a name="example"></a>Esempio  
 Il codice riportato in questo esempio crea oggetti `SqlCommand` e `SqlParameter` per l'inserimento di dati in una colonna con tipo definito dall'utente di una tabella. Il codice utilizza l'enumerazione `SqlDbType.Udt` per specificare il tipo di dati e la proprietà `UdtTypeName` dell'oggetto `SqlParameter` per specificare il nome completo del tipo definito dall'utente nel database.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai tipi definiti dall'utente in ADO.NET](accessing-user-defined-types-in-ado-net.md)  
  
  
