---
title: Funzioni a valori scalari CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: cf5c0b6c7004f458e424e58d738cce22e97afa2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919594"
---
# <a name="clr-scalar-valued-functions"></a>Funzioni a valori scalari CLR
  Una funzione a valori scalari restituisce un valore singolo, come una stringa un Integer o un valore di bit. È possibile creare funzioni a valori scalari definite dall'utente nel codice gestito utilizzando qualsiasi linguaggio di programmazione di .NET Framework. Queste funzioni sono accessibili a [!INCLUDE[tsql](../../includes/tsql-md.md)] o ad altro codice gestito. Per informazioni sui vantaggi dell'integrazione con CLR e sulla scelta tra codice gestito [!INCLUDE[tsql](../../includes/tsql-md.md)]e, vedere [Cenni preliminari sull'integrazione con CLR](../clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Requisiti per le funzioni a valori scalari CLR  
 Le funzioni a valori scalari di .NET Framework vengono implementate come metodi in una classe di un assembly .NET Framework. I parametri di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]input e il tipo restituiti da un SVF possono essere uno qualsiasi dei tipi di dati scalari supportati `varchar`da `char`, `rowversion`ad `text`eccezione `ntext`di `image`, `timestamp`, `table`,, `cursor`,,, o. Le funzioni a valori scalari devono assicurare una corrispondenza tra il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il tipo dati restituito del metodo di implementazione. Per ulteriori informazioni sulle conversioni di tipi, vedere [mapping dei dati dei parametri CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 In caso di implementazione di una funzione a valore scalare di .NET Framework in un linguaggio di .NET Framework, è possibile specificare l'attributo personalizzato `SqlFunction` per includere informazioni aggiuntive sulla funzione. L'attributo `SqlFunction` indica se la funzione accede ai dati o li modifica, se è deterministica e se comporta operazioni a virgola mobile.  
  
 Le funzioni definite dall'utente a valori scalari possono essere deterministiche o non deterministiche. Una funzione deterministica restituisce sempre lo stesso risultato quando viene chiamata con un set specifico di parametri di input. Una funzione non deterministica può restituire risultati diversi quando viene chiamata con un set specifico di parametri di input.  
  
> [!NOTE]  
>  Non contrassegnare una funzione come deterministica se non produce sempre gli stessi valori di output, dati gli stessi valori di input e lo stesso stato del database. Una funzione non propriamente deterministica ma contrassegnata come tale può causare danni a viste indicizzate e colonne calcolate. Per contrassegnare una funzione come deterministica, impostare la proprietà `IsDeterministic` su true.  
  
### <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella, ovvero tipi di tabella definiti dall'utente passati in una procedura o in una funzione, consentono di passare in modo efficiente più righe di dati al server. Pur essendo caratterizzati da funzionalità simili alle matrici di parametri, i parametri con valori di tabella offrono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella consentono inoltre di ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. Per altre informazioni su TVP, vedere [usare i parametri con valori di tabella &#40;motore di database&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
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
  
 La prima riga di codice fa riferimento a `Microsoft.SqlServer.Server` per accedere ad attributi e a `System.Data.SqlClient` per accedere allo spazio dei nomi ADO.NET. Questo spazio dei nomi contiene `SqlClient`, il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Dopodiché, la funzione riceve l'attributo personalizzato `SqlFunction`, presente nello spazio dei nomi `Microsoft.SqlServer.Server`. L'attributo personalizzato indica se la funzione definita dall'utente utilizza il provider in-process per leggere dati nel server. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente alle Funzioni definite dall'utente di aggiornare, inserire o eliminare dati. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono ottimizzare l'esecuzione di una UDF che non utilizza il provider in-process. Questa possibilità viene indicata impostando `DataAccessKind` su `DataAccessKind.None`. Sulla riga successiva il metodo di destinazione è un metodo statico pubblico (condiviso in Visual Basic .NET).  
  
 La classe `SqlContext`, che si trova nello spazio dei nomi `Microsoft.SqlServer.Server`, può quindi accedere a un oggetto `SqlCommand` con una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] già configurata. Sebbene non venga utilizzato qui, il contesto della transazione corrente è disponibile anche tramite l'API (Application Programming Interface) di `System.Transactions`.  
  
 La maggior parte delle righe di codice nel corpo della funzione è già nota agli sviluppatori che hanno scritto applicazioni client che utilizzano i tipi presenti nello spazio dei nomi `System.Data.SqlClient`.  
  
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
  
 Il testo del comando appropriato viene specificato inizializzando l'oggetto `SqlCommand`. Nell'esempio precedente viene contato il numero di righe nella tabella `SalesOrderHeader`. Dopodiché, viene chiamato il metodo `ExecuteScalar` dell'oggetto `cmd`. Viene quindi restituito un valore di tipo `int` basato sulla query. Infine, il numero di ordini viene restituito al chiamante.  
  
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
>  
  `/t:library` indica che è necessario generare una libreria anziché un file eseguibile. I file eseguibili non possono essere registrati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  L'esecuzione degli oggetti di database Visual C++ compilati con `/clr:pure` non è più supportata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo tipo di oggetti di database include, ad esempio, funzioni a valori scalari.  
  
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
 [Mapping dei dati dei parametri CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Panoramica degli attributi personalizzati dell'integrazione con CLR](../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)   
 [Funzioni definite dall'utente](../user-defined-functions/user-defined-functions.md)   
 [Accesso ai dati da oggetti di database CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
