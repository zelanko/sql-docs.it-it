---
title: Statistiche del provider per SQL Server
description: Viene descritto il supporto per ottenere SQL Server statistiche di run-time.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 092cf63e62bce01e2a771ce4e5f7f46e1073e91a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452059"
---
# <a name="provider-statistics-for-sql-server"></a>Statistiche del provider per SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A partire da .NET Framework versione 2,0 e .NET Core versione 1,0, Microsoft SqlClient provider di dati per SQL Server supporta le statistiche di run-time. È necessario abilitare le statistiche impostando la proprietà <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> dell'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> su `True` dopo che è stato creato un oggetto connessione valido. Una volta abilitate le statistiche, è possibile esaminarle come "snapshot nel tempo" recuperando un riferimento <xref:System.Collections.IDictionary> tramite il metodo <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> dell'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection>. È possibile enumerare l'elenco come un set di voci del dizionario delle coppie nome/valore. Queste coppie nome/valore non sono ordinate. In qualsiasi momento, è possibile chiamare il metodo di <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> dell'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> per reimpostare i contatori. Se la raccolta delle statistiche non è stata abilitata, non viene generata un'eccezione. Inoltre, se <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> viene chiamato senza <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> chiamato per primo, i valori recuperati sono i valori iniziali per ogni voce. Se si abilitano le statistiche, si esegue l'applicazione per un periodo di tempo e si disabilitano le statistiche, i valori recuperati rifletteranno i valori raccolti fino al punto in cui le statistiche sono state disabilitate. Tutti i valori statistici raccolti sono in base alla connessione.  
  
## <a name="statistical-values-available"></a>Valori statistici disponibili  
Attualmente sono disponibili 18 elementi diversi dal provider Microsoft SQL Server. È possibile accedere alle voci disponibili tramite la proprietà **Count** del riferimento dell'interfaccia <xref:System.Collections.IDictionary> restituito da <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>. Tutti i contatori delle statistiche del provider usano il tipo <xref:System.Int64> di Common Language Runtime (**long** in C# e Visual Basic), da 64 bit. Il valore massimo del tipo di dati **int64**, definito dal campo **int64.MaxValue**, è ((2^63)-1)). Quando i valori per i contatori raggiungono questo valore massimo, non devono più essere considerati accurati. Ciò significa che **int64.MaxValue**-1((2^63)-2) è realmente il valore massimo valido per le statistiche.  
  
> [!NOTE]
>  Un dizionario viene utilizzato per restituire le statistiche del provider perché il numero, i nomi e l'ordine delle statistiche restituite possono cambiare in futuro. Le applicazioni non devono basarsi su un valore specifico trovato nel dizionario, ma devono invece verificare se il valore è presente e creare un ramo di conseguenza.  
  
Nella tabella seguente vengono descritti i valori statistici correnti disponibili. Si noti che i nomi delle chiavi per i singoli valori non sono localizzati nelle versioni internazionali di Microsoft .NET Framework e .NET Core.  
  
|Nome chiave|Descrizione|  
|--------------|-----------------|  
|`BuffersReceived`|Restituisce il numero di pacchetti TDS (Tabular Data Stream) ricevuti dal provider dal SQL Server dopo che l'applicazione è stata avviata utilizzando il provider e ha abilitato le statistiche.|  
|`BuffersSent`|Restituisce il numero di pacchetti TDS inviati a SQL Server dal provider dopo che sono state abilitate le statistiche. I comandi di grandi dimensioni possono richiedere più buffer. Se, ad esempio, un comando di grandi dimensioni viene inviato al server e richiede sei pacchetti, `ServerRoundtrips` viene incrementato di uno e `BuffersSent` viene incrementato di sei.|  
|`BytesReceived`|Restituisce il numero di byte di dati nei pacchetti TDS ricevuti dal provider da SQL Server dopo che l'applicazione è stata avviata utilizzando il provider e ha abilitato le statistiche.|  
|`BytesSent`|Restituisce il numero di byte di dati inviati a SQL Server nei pacchetti TDS dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate.|  
|`ConnectionTime`|Il periodo di tempo (in millisecondi) durante il quale la connessione è stata aperta dopo l'abilitazione delle statistiche (tempo di connessione totale se le statistiche sono state abilitate prima di aprire la connessione).|  
|`CursorOpens`|Restituisce il numero di volte in cui un cursore è stato aperto tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate.<br /><br /> Si noti che i risultati di sola lettura o di solo invio restituiti dalle istruzioni SELECT non sono considerati cursori e pertanto non influiscono su questo contatore.|  
|`ExecutionTime`|Restituisce l'intervallo di tempo cumulativo (in millisecondi) usato dal provider per l'elaborazione dopo l'abilitazione delle statistiche, incluso il tempo di attesa per le risposte del server nonché il tempo di esecuzione del codice nel provider stesso.<br /><br /> Le classi che includono il codice temporale sono:<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> Per ridurre il più possibile i membri critici per le prestazioni, i membri seguenti non sono temporizzati:<br /><br /> SqlDataReader<br /><br /> operatore [] (tutti gli overload)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|Restituisce il numero totale di istruzioni INSERT, DELETE e UPDATE eseguite tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider ed è stata abilitata la funzionalità Statistics.|  
|`IduRows`|Restituisce il numero totale di righe interessate dalle istruzioni INSERT, DELETE e UPDATE eseguite tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider ed è stata abilitata la funzionalità Statistics.|  
|`NetworkServerTime`|Restituisce il tempo cumulativo (in millisecondi) di attesa del provider per le risposte dal server dopo che l'avvio dell'applicazione e l'abilitazione delle statistiche.|  
|`PreparedExecs`|Restituisce il numero di comandi preparati eseguiti tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate.|  
|`Prepares`|Restituisce il numero di istruzioni preparate tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider ed è stata abilitata la statistica.|  
|`SelectCount`|Restituisce il numero di istruzioni SELECT eseguite tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate. Sono incluse le istruzioni FETCH per recuperare le righe dai cursori e il conteggio delle istruzioni SELECT viene aggiornato quando viene raggiunta la fine di un <xref:Microsoft.Data.SqlClient.SqlDataReader>.|  
|`SelectRows`|Restituisce il numero di righe selezionate dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate. Questo contatore riflette tutte le righe generate da istruzioni SQL, anche quelle che non sono state effettivamente utilizzate dal chiamante. La chiusura di un lettore di dati prima della lettura dell'intero set di risultati, ad esempio, non influisce sul conteggio. Sono incluse le righe recuperate dai cursori tramite istruzioni FETCH.|  
|`ServerRoundtrips`|Restituisce il numero di volte in cui la connessione ha inviato comandi al server e ha restituito una risposta dopo che l'applicazione è stata avviata utilizzando il provider e ha abilitato le statistiche.|  
|`SumResultSets`|Restituisce il numero di set di risultati utilizzati dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate. Ad esempio, questo includerebbe tutti i set di risultati restituiti al client. Per i cursori, ogni operazione di recupero o blocco di recupero viene considerata un set di risultati indipendente.|  
|`Transactions`|Restituisce il numero di transazioni utente avviate dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate, inclusi i rollback. Se una connessione è in esecuzione con commit automatico in, ogni comando viene considerato una transazione.<br /><br /> Questo contatore incrementa il conteggio delle transazioni non appena viene eseguita un'istruzione BEGIN TRAN, indipendentemente dal fatto che venga eseguito il commit o il rollback della transazione in un secondo momento.|  
|`UnpreparedExecs`|Restituisce il numero di istruzioni non preparate eseguite tramite la connessione dopo che l'applicazione è stata avviata utilizzando il provider e le statistiche sono state abilitate.|  
  
### <a name="retrieving-a-value"></a>Recupero di un valore  
Nell'applicazione console seguente viene illustrato come abilitare le statistiche su una connessione, recuperare quattro singoli valori statistici e scriverli nella finestra della console.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in SQL Server. Per la stringa di connessione fornita nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale. Modificare la stringa di connessione in modo che sia necessario per l'ambiente in uso.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>Recupero di tutti i valori  
Nell'applicazione console seguente viene illustrato come abilitare le statistiche su una connessione, recuperare tutti i valori statistici disponibili utilizzando l'enumeratore e scriverli nella finestra della console.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in SQL Server. Per la stringa di connessione fornita nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale. Modificare la stringa di connessione in modo che sia necessario per l'ambiente in uso.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
