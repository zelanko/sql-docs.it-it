---
title: 'Passaggio 4: Connettersi in modo resiliente a SQL con ADO.NET | Microsoft Docs'
description: Viene descritto come connettersi in modo resiliente a SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-kaywon
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: rothja
ms.author: jroth
ms.openlocfilehash: b52267870338065589de9bb54e5a332b923348fd
ms.sourcegitcommit: d876425e5c465ee659dd54e7359cda0d993cbe86
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/24/2020
ms.locfileid: "77568100"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Passaggio 4: Connettersi in modo resiliente a SQL con ADO.NET

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Scaricare ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- Articolo precedente:&nbsp;&nbsp;&nbsp;[Passaggio 3: Modello di verifica per la connessione a SQL con ADO.NET](step-3-connect-sql-ado-net.md)  

  
In questo argomento viene fornito un esempio di codice C# che illustra una logica di ripetizione dei tentativi personalizzata. La logica di ripetizione dei tentativi garantisce affidabilità. È progettata per elaborare correttamente gli errori o *guasti temporanei* che tendono a risolversi se il programma attende qualche secondo ed effettua un nuovo tentativo.  
  
L'origine di un errore temporaneo può essere:  
  
- Un errore di breve durata della rete che supporta Internet.  
- Il bilanciamento del carico delle risorse di un sistema cloud al momento dell'invio della query.  
  
  
Le classi ADO.NET per la connessione all'istanza locale di Microsoft SQL Server possono anche connettersi al database SQL di Azure. Tuttavia, le classi ADO.NET non forniscono autonomamente tutta la solidità e l’affidabilità necessarie per l’uso in un ambiente di produzione. Il programma client può incorrere in guasti temporanei da cui deve poter eseguire un ripristino automatico e continuare a funzionare.  
  
## <a name="step-1-identify-transient-errors"></a>Passaggio 1: Identificare gli errori temporanei  
  
Il programma deve distinguere gli errori temporanei dagli errori persistenti. Gli errori temporanei sono condizioni di errore che possono scomparire entro un breve periodo di tempo, ad esempio problemi momentanei della rete.  Un esempio di errore persistente può essere l'uso da parte del programma di un nome scritto in modo errato per il database di destinazione: in questo caso l'errore "Database non trovato" è persistente e non è possibile cancellarlo entro un breve periodo di tempo.  
  
L'elenco dei numeri di errore classificati come errori temporanei è disponibile nell'elenco dei [messaggi di errore per le applicazioni client del database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)   
  
## <a name="step-2-create-and-run-sample-application"></a>Passaggio 2: Creare ed eseguire un'applicazione di esempio  
  
In questo esempio si presuppone che sia installato .NET Framework 4.5.1 o versione successiva.  L'esempio di codice C# è costituito da un file denominato Program.cs. Il relativo codice viene specificato nella sezione successiva.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Passaggio 2.a: Acquisire e compilare il codice di esempio  
  
È possibile compilare l'esempio con i passaggi seguenti:  
  
1. Nell’ [edizione gratuita Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs), creare un nuovo progetto dal modello di applicazione Console C#.  
    - File > Nuovo > Progetto > Installati > Modelli > Visual C# > Windows > Desktop classico > Applicazione console  
    - Assegnare al progetto il nome **RetryAdo2**.  
2. Aprire il riquadro Esplora soluzioni.  
    - Visualizzare il nome del progetto.  
    - Visualizzare il nome del file Program.cs.  
3. Aprire il file Program.cs.  
4. Sostituire completamente il contenuto del file Program.cs con il codice nel blocco di codice seguente.  
5. Fare clic sul menu Compilazione > Compila soluzione.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Passaggio 2.b: Copiare e incollare il codice di esempio  
  
Incollare questo codice nel file **Program.cs** .  
  
È necessario modificare le stringhe per nome del server, password e così via. È possibile trovare queste stringhe nel metodo denominato **GetSqlConnectionStringBuilder**.  
  
NOTA:  La stringa di connessione per il nome del server è pensata per il database SQL di Azure, perché include il prefisso di quattro caratteri di **tcp:**, ma è possibile modificare la stringa del server per connettersi a Microsoft SQL Server.  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
using TD = System.Threading;  
    
namespace RetryAdo2  
{  
  public class Program  
  {  
    static public int Main(string[] args)  
    {  
      bool succeeded = false;  
      int totalNumberOfTimesToTry = 4;  
      int retryIntervalSeconds = 10;  
    
      for (int tries = 1;  
        tries <= totalNumberOfTimesToTry;  
        tries++)  
      {  
        try  
        {  
          if (tries > 1)  
          {  
            Console.WriteLine  
              ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
              tries, totalNumberOfTimesToTry  
              );  
            TD.Thread.Sleep(1000 * retryIntervalSeconds);  
            retryIntervalSeconds = Convert.ToInt32  
              (retryIntervalSeconds * 1.5);  
          }  
          AccessDatabase();  
          succeeded = true;  
          break;  
        }  
    
        catch (QC.SqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (TestSqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (Exception Exc)  
        {  
          Console.WriteLine(Exc);  
          succeeded = false;  
          break;  
        }  
      }  
    
      if (succeeded == true)  
      {  
        return 0;  
      }  
      else  
      {  
        Console.WriteLine("ERROR: Unable to access the database!");  
        return 1;  
      }  
    }  
    
    /// <summary>  
    /// Connects to the database, reads,  
    /// prints results to the console.  
    /// </summary>  
    static public void AccessDatabase()  
    {  
      //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
    
      using (var sqlConnection = new QC.SqlConnection  
          (GetSqlConnectionString()))  
      {  
        using (var dbCommand = sqlConnection.CreateCommand())  
        {  
          dbCommand.CommandText = @"  
SELECT TOP 3  
    ob.name,  
    CAST(ob.object_id as nvarchar(32)) as [object_id]  
  FROM sys.objects as ob  
  WHERE ob.type='IT'  
  ORDER BY ob.name;";  
    
          sqlConnection.Open();  
          var dataReader = dbCommand.ExecuteReader();  
    
          while (dataReader.Read())  
          {  
            Console.WriteLine("{0}\t{1}",  
              dataReader.GetString(0),  
              dataReader.GetString(1));  
          }  
        }  
      }  
    }  
    
    /// <summary>  
    /// You must edit the four 'my' string values.  
    /// </summary>  
    /// <returns>An ADO.NET connection string.</returns>  
    static private string GetSqlConnectionString()  
    {  
      // Prepare the connection string to Azure SQL Database.  
      var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
    
      // Change these values to your values.  
      sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
      sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
    
      sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
      sqlConnectionSB.Password = "MyPassword";  
      sqlConnectionSB.IntegratedSecurity = false;  
    
      // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
      sqlConnectionSB.ConnectRetryCount = 3;  
      sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
    
      // Leave these values as they are.  
      sqlConnectionSB.IntegratedSecurity = false;  
      sqlConnectionSB.Encrypt = true;  
      sqlConnectionSB.ConnectTimeout = 30;  
    
      return sqlConnectionSB.ToString();  
    }  
    
    static public CG.List<int> TransientErrorNumbers =  
      new CG.List<int> { 4060, 40197, 40501, 40613,  
      49918, 49919, 49920, 11001 };  
  }  
    
  /// <summary>  
  /// For testing retry logic, you can have method  
  /// AccessDatabase start by throwing a new  
  /// TestSqlException with a Number that does  
  /// or does not match a transient error number  
  /// present in TransientErrorNumbers.  
  /// </summary>  
  internal class TestSqlException : ApplicationException  
  {  
    internal TestSqlException(int testErrorNumber)  
    { this.Number = testErrorNumber; }  
    
    internal int Number  
    { get; set; }  
  }  
}  
```  
  
###  <a name="step-2c-run-the-program"></a>Passaggio 2.c: Eseguire il programma  
  
  
L’eseguibile **RetryAdo2.exe** non invia parametri. Per eseguire il file EXE:  
  
1. Aprire una finestra della console in cui è stato compilato il file binario RetryAdo2.exe.  
2. Eseguire RetryAdo2.exe senza parametri di input.  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Passaggio 3: Come testare la logica di ripetizione dei tentativi  
  
Per testare la logica di ripetizione dei tentativi è possibile simulare un errore temporaneo in diversi modi.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Passaggio 3.a: Generare un'eccezione di test  
  
L'esempio di codice include:  
  
- Una piccola seconda classe denominata **TestSqlException**, con la proprietà **Number**.  
- `//throw new TestSqlException(4060);` , da cui è possibile rimuovere il commento.  
  
Se si rimuove il commento dall'istruzione throw e si ricompila, l'esecuzione successiva di **RetryAdo2.exe** restituisce un output simile al seguente.  
  
```  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>> RetryAdo2.exe  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 2 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 3 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 4 of 4 max...  
4060: transient occurred. (TESTING.)  
ERROR: Unable to access the database!  
  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Passaggio 3.b: Eseguire nuovamente il test con un errore persistente  
  
Per verificare se il codice gestisce correttamente gli errori persistenti, rieseguire il test precedente facendo attenzione a non usare il numero di un errore temporaneo effettivo, come 4060. Usare invece il numero fittizio 7654321. Il programma deve trattarlo come un errore persistente e ignorare qualsiasi ripetizione dei tentativi.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Passaggio 3.c: Disconnettersi dalla rete  
  
1. Disconnettere il computer client dalla rete.  
    - In un computer desktop scollegare il cavo di rete.  
    - In un computer portatile premere la combinazione di tasti funzione che disattiva la scheda di rete.  
2. Avviare RetryAdo2.exe e attendere che venga visualizzato il primo errore temporaneo, probabilmente il numero 11001.  
3. Riconnettersi alla rete mentre RetryAdo2.exe è ancora in esecuzione.  
4. La console segnalerà l'esito positivo di un tentativo successivo.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Passaggio 2.d: Specificare temporaneamente il nome del server in modo errato  
  
1. Aggiungere temporaneamente il numero di errore 40615 a **TransientErrorNumbers**e ricompilare.  
2. Impostare un punto di interruzione sulla riga `new QC.SqlConnectionStringBuilder()`.  
3. Usare la funzionalità *Modifica e continuazione* per specificare intenzionalmente in modo errato il nome del server un paio di righe più in basso.  
    - Consentire l'esecuzione del programma e tornare al punto di interruzione.  
    - Si verifica l'errore 40615.  
4. Correggere l'errore di ortografia.  
5. Consentire l'esecuzione e il completamento del programma.  
6. Rimuovere il numero 40615 e ricompilare.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
Per esplorare altre procedure consigliate e linee guida per la progettazione, vedere [Connessione al database SQL: collegamenti, procedure consigliate e linee guida per la progettazione](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
