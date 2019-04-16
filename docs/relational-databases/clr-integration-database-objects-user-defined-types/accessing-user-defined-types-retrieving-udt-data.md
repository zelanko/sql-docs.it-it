---
title: Il recupero dei dati di tipo definito dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: d6b70a61173de35d441208dc5f2794e5d5b341ed
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582964"
---
# <a name="accessing-user-defined-types---retrieving-udt-data"></a>Accesso ai tipi definiti dall'utente - Recupero di dati UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per creare un tipo definito dall'utente (UDT) nel client, l'assembly registrato come tipo definito dall'utente in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere disponibile per l'applicazione client. L'assembly UDT può essere posizionato nella stessa directory dell'applicazione oppure nella Global Assembly Cache (GAC). È inoltre possibile impostare un riferimento all'assembly nel progetto.  
  
## <a name="requirements-for-using-udts-in-adonet"></a>Requisiti per l'utilizzo di tipi definiti dall'utente in ADO.NET  
 Per consentire la creazione del tipo definito dall'utente sul client, è necessario che l'assembly caricato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'assembly sul client siano compatibili. Per tipi definiti dall'utente definito con la **nativa** formato di serializzazione, gli assembly devono essere strutturalmente compatibili. Per gli assembly definiti con la **UserDefined** formato, l'assembly deve essere disponibile nel client.  
  
 Per recuperare i dati non elaborati da una colonna con tipo definito dall'utente in una tabella, non è necessario che sul client sia disponibile una copia dell'assembly UDT.  
  
> [!NOTE]  
>  **SqlClient** potrebbe non riuscire a caricare un tipo definito dall'utente in caso di versioni non corrispondenti di tipo definito dall'utente o altri problemi. In questo caso, utilizzare i normali meccanismi per la risoluzione di problemi per determinare il motivo per cui l'assembly in cui è contenuto il tipo definito dall'utente non viene individuato dall'applicazione chiamante. Per ulteriori informazioni, consultare l'argomento intitolato "Diagnostica degli errori tramite gli assistenti al debug gestito" nella documentazione di .NET Framework.  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>Accesso ai tipi definiti dall'utente con un oggetto SqlDataReader  
 Oggetto **SqlClient. SqlDataReader** utilizzabile dal codice client per recuperare un set di risultati contenente una colonna di tipo definito dall'utente, che viene esposta come un'istanza dell'oggetto.  
  
### <a name="example"></a>Esempio  
 Questo esempio illustra come usare il **Main** per creare un nuovo metodo **SqlDataReader** oggetto. All'interno del codice di esempio si verificano le azioni seguenti:  
  
1.  Il metodo Main crea un nuovo **SqlDataReader** dell'oggetto e recupera i valori della tabella Points, che include una colonna di tipo definito dall'utente denominata Point.  
  
2.  Il tipo definito dall'utente di Point espone le coordinate X e Y definite come numeri interi.  
  
3.  Il tipo definito dall'utente definisce una **distanza** metodo e un **GetDistanceFromXY** (metodo).  
  
4.  Il codice di esempio recupera i valori delle colonne con tipo definito dall'utente di chiave primaria per dimostrare le funzionalità del tipo definito dall'utente.  
  
5.  Il codice di esempio chiama il **Point.Distance** e **GetDistanceFromXY** metodi.  
  
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
 In alcune situazioni può risultare utile recuperare i dati non elaborati dalla colonna con tipo definito dall'utente. Può accadere che il tipo non sia disponibile localmente o non si desideri creare un'istanza del tipo definito dall'utente. È possibile leggere i byte non elaborati in una matrice di byte utilizzando il **GetBytes** metodo di un **SqlDataReader**. Tale metodo legge un flusso di byte dall'offset di colonna specificato nel buffer di una matrice, a partire dall'offset del buffer specificato. Un'altra opzione consiste nell'usare uno dei **GetSqlBytes** oppure **GetSqlBinary** metodi e leggere tutto il contenuto in un'unica operazione. In entrambi i casi non viene mai creata un'istanza dell'oggetto UDT, pertanto non è necessario impostare un riferimento al tipo definito dall'utente nell'assembly client.  
  
### <a name="example"></a>Esempio  
 In questo esempio mostra come recuperare il **punto** i dati come byte non elaborati in una matrice di byte utilizzando un **SqlDataReader**. Il codice Usa un **StringBuilder** per convertire i byte non elaborati in una rappresentazione di stringa da visualizzare nella finestra della console.  
  
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
 In questo esempio mostra come recuperare il **punto** i dati come byte non elaborati in una singola operazione utilizzando il **GetSqlBytes** (metodo). Il codice Usa un **StringBuilder** per convertire i byte non elaborati in una rappresentazione di stringa da visualizzare nella finestra della console.  
  
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
 Tipi definiti dall'utente da utilizzare come valori dei parametri quando si configura un **SqlParameter** per una **System.Data.SqlClient.SqlCommand** oggetto. Il **SqlDbType. UDT** enumerazione di una **SqlParameter** oggetto viene usato per indicare che il parametro è un tipo definito dall'utente quando si chiama il **Add** metodo per il  **Parametri** raccolta. Il **UdtTypeName** proprietà di un **SqlCommand** oggetto viene usato per specificare il nome completo del tipo in questione nel database utilizzando il *schema_name* sintassi. Anche se non è richiesto, l'utilizzo che il nome completo, elimina l'ambiguità dal codice.  
  
> [!NOTE]  
>  Una copia locale dell'assembly UDT deve essere disponibile per il progetto client.  
  
### <a name="example"></a>Esempio  
 Nel codice in questo esempio viene creato **SqlCommand** e **SqlParameter** oggetti per inserire dati in una colonna di tipo definito dall'utente in una tabella. Il codice Usa il **SqlDbType. UDT** enumerazione per specificare il tipo di dati e il **UdtTypeName** proprietà del **SqlParameter** oggetto per specificare il nome completo del tipo definito dall'utente nel database.  
  
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
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      
      param.UdtTypeName = "TestPoint.dbo.Point"      
      param.Direction = ParameterDirection.Input      
      param.Value = New Point(5, 6)      
      cmd.Parameters.Add(param)  
  
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
 [Accesso ai tipi definiti dall'utente in ADO.NET](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
  
  
