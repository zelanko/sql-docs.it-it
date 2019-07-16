---
title: Le funzioni a valori scalari CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
ms.openlocfilehash: ac063fa59d22308cb90206816555eea8474acca6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009778"
---
# <a name="clr-scalar-valued-functions"></a>Funzioni a valori scalari CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una funzione a valori scalari restituisce un valore singolo, come una stringa un Integer o un valore di bit. È possibile creare funzioni a valori scalari definite dall'utente nel codice gestito utilizzando qualsiasi linguaggio di programmazione di .NET Framework. Queste funzioni sono accessibili a [!INCLUDE[tsql](../../includes/tsql-md.md)] o ad altro codice gestito. Per informazioni sui vantaggi dell'integrazione con CLR e sulla scelta tra codice gestito e [!INCLUDE[tsql](../../includes/tsql-md.md)], vedere [panoramica dell'integrazione con CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Requisiti per le funzioni a valori scalari CLR  
 Le funzioni a valori scalari di .NET Framework vengono implementate come metodi in una classe di un assembly .NET Framework. I parametri di input e il tipo restituito da un file SVF può essere uno dei tipi di dati scalari supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tranne **varchar**, **char**, **rowversion**, **testo**, **ntext**, **immagine**, **timestamp**, **tabella**, o **cursore** . Le funzioni a valori scalari devono assicurare una corrispondenza tra il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il tipo dati restituito del metodo di implementazione. Per altre informazioni sulle conversioni dei tipi, vedere [Mapping dei dati dei parametri CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Quando si implementa un Scalari di .NET Framework in un linguaggio di .NET Framework, il **SqlFunction** attributo personalizzato può essere specificato per includere informazioni aggiuntive sulla funzione. Il **SqlFunction** attributo indica se la funzione accede o modifica i dati, se è deterministica e se comporta operazioni a virgola mobile.  
  
 Le funzioni definite dall'utente a valori scalari possono essere deterministiche o non deterministiche. Una funzione deterministica restituisce sempre lo stesso risultato quando viene chiamata con un set specifico di parametri di input. Una funzione non deterministica può restituire risultati diversi quando viene chiamata con un set specifico di parametri di input.  
  
> [!NOTE]  
>  Non contrassegnare una funzione come deterministica se non produce sempre gli stessi valori di output, dati gli stessi valori di input e lo stesso stato del database. Una funzione non propriamente deterministica ma contrassegnata come tale può causare danni a viste indicizzate e colonne calcolate. Si contrassegna una funzione come deterministica impostando il **IsDeterministic** proprietà su true.  
  
### <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella, ovvero tipi di tabella definiti dall'utente passati in una procedura o in una funzione, consentono di passare in modo efficiente più righe di dati al server. Pur essendo caratterizzati da funzionalità simili alle matrici di parametri, i parametri con valori di tabella offrono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella consentono inoltre di ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. Per altre informazioni sulle TVP, vedere [usare parametri &#40;motore di Database&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>Esempio di una funzione a valori scalari CLR  
 Di seguito è riportata una semplice funzione a valori scalari che accede ai dati e restituisce un valore integer:  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 La prima riga dei riferimenti al codice **SQLServer** per accedere agli attributi e **SqlClient** accedere lo spazio dei nomi ADO.NET. (Questo spazio dei nomi contiene **SqlClient**, il Provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 Successivamente, la funzione riceve la **SqlFunction** attributo personalizzato, situata nella **SQLServer** dello spazio dei nomi. L'attributo personalizzato indica se la funzione definita dall'utente utilizza il provider in-process per leggere dati nel server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente alle Funzioni definite dall'utente di aggiornare, inserire o eliminare dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono ottimizzare l'esecuzione di una UDF che non utilizza il provider in-process. Ciò viene indicato impostando **DataAccessKind** al **DataAccessKind. None**. Sulla riga successiva il metodo di destinazione è un metodo statico pubblico (condiviso in Visual Basic .NET).  
  
 Il **SqlContext** (classe), che si trova nel **SQLServer** dello spazio dei nomi, quindi è possibile accedere una **SqlCommand** oggetto con una connessione al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza che è già stato configurato. Anche se non utilizzato in questo caso, il contesto della transazione corrente è disponibile anche tramite il **System. Transactions** (API) application programming interface.  
  
 La maggior parte delle righe di codice nel corpo della funzione dovrebbe essere familiare agli sviluppatori che hanno scritto applicazioni client che utilizzano i tipi presenti nel **SqlClient** dello spazio dei nomi.  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 Il testo del comando appropriato viene specificato inizializzando il **SqlCommand** oggetto. Nell'esempio precedente viene contato il numero di righe nella tabella **SalesOrderHeader**. Successivamente, il **ExecuteScalar** metodo il **cmd** viene chiamato l'oggetto. Questo metodo restituisce un valore di tipo **int** basato sulla query. Infine, il numero di ordini viene restituito al chiamante.  
  
 Se questo codice viene salvato in un file chiamato FirstUdf.cs, può essere compilato come assembly nel modo seguente:  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` indica che è necessario generare una libreria anziché un file eseguibile. I file eseguibili non possono essere registrati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Gli oggetti di database Visual C++ compilati con **/clr: pure** non sono supportati per l'esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo tipo di oggetti di database include, ad esempio, funzioni a valori scalari.  
  
 Di seguito sono riportate la query [!INCLUDE[tsql](../../includes/tsql-md.md)] e una chiamata di esempio per registrare l'assembly e la funzione definita dall'utente.  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 Si noti che il nome della funzione esposto in [!INCLUDE[tsql](../../includes/tsql-md.md)] non dovere corrispondere al nome del metodo statico pubblico di destinazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping dei dati dei parametri CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Panoramica degli attributi personalizzati di integrazione CLR](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [Funzioni definite dall'utente](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [Accesso ai dati da oggetti di database CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
