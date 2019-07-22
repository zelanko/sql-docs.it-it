---
title: 'Passaggio 4: connettersi in modo resiliente a SQL con ADO.NET | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a080f68497829657c60bbd96238b71123b70d87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957591"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Passaggio 4: Connettersi in modo resiliente a SQL con ADO.NET

- Articolo precedente:&nbsp;&nbsp;&nbsp;[Passaggio 3: Modello di verifica per la connessione a SQL con ADO.NET](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
In questo argomento viene C# fornito un esempio di codice che illustra la logica di ripetizione dei tentativi personalizzata. La logica di ripetizione dei tentativi garantisce affidabilità. La logica di ripetizione dei tentativi è progettata per elaborare normalmente errori *temporanei o errori* temporanei che tendono a scomparire se il programma attende diversi secondi e nuovi tentativi.  
  
Le origini degli errori temporanei includono:  
  
- Un breve errore della rete che supporta Internet.  
- Un sistema cloud potrebbe bilanciare il carico delle risorse al momento dell'invio della query.  
  
  
Le classi ADO.NET per la connessione al Microsoft SQL Server locale possono anche connettersi al database SQL di Azure. Tuttavia, le classi ADO.NET non possono fornire tutta la solidità e l'affidabilità necessarie per l'uso in produzione. Il programma client può rilevare errori temporanei da cui deve essere ripristinato in modo invisibile all'utente e continuarsi autonomamente.  
  
## <a name="step-1-identify-transient-errors"></a>Passaggio 1: identificare gli errori temporanei  
  
Il programma deve distinguere tra gli errori temporanei e gli errori persistenti. Gli errori temporanei sono condizioni di errore che possono risultare evidenti entro un breve periodo di tempo, ad esempio problemi di rete temporanei.  Un esempio di errore persistente è che, se il programma ha un errore di ortografia del nome del database di destinazione, in questo caso l'errore "nessun database di questo tipo è stato trovato" e non è possibile cancellarlo entro un breve periodo di tempo.  
  
L'elenco dei numeri di errore categorizzati come errori temporanei è disponibile nei [messaggi di errore per le applicazioni client del database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Passaggio 2: creare ed eseguire un'applicazione di esempio  
  
In questo esempio si presuppone che sia installato .NET Framework 4.5.1 o versione successiva.  L' C# esempio di codice è costituito da un file denominato Program.cs. Il codice è disponibile nella sezione successiva.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Passaggio 2. a: acquisire e compilare l'esempio di codice  
  
È possibile compilare l'esempio con i passaggi seguenti:  
  
1. Nell' [edizione gratuita di Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs)creare un nuovo progetto dal modello di C# applicazione console.  
    - File > nuovo progetto > > installato > modelli > applicazione C# console > desktop classico > Visual > Windows  
    - Denominare il progetto **RetryAdo2**.  
2. Aprire il riquadro Esplora soluzioni.  
    - Vedere il nome del progetto.  
    - Vedere il nome del file Program.cs.  
3. Aprire il file Program.cs.  
4. Sostituire completamente il contenuto del file Program.cs con il codice nel blocco di codice seguente.  
5. Fare clic sul menu Compila > Compila soluzione.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Passaggio 2. b: copiare e incollare il codice di esempio  
  
Incollare questo codice nel file **Program.cs** .  
  
È quindi necessario modificare le stringhe per nome server, password e così via. È possibile trovare queste stringhe nel metodo denominato **GetSqlConnectionStringBuilder**.  
  
Nota: la stringa di connessione per il nome del server è orientata al database SQL di Azure, perché include il prefisso di quattro caratteri **TCP:** . È tuttavia possibile modificare la stringa del server per connettersi al Microsoft SQL Server.  
  
  
```csharp
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
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
  
###  <a name="step-2c-run-the-program"></a>Passaggio 2. c: eseguire il programma  
  
  
L'eseguibile **RetryAdo2. exe** non immette parametri. Per eseguire il file con estensione exe:  
  
1. Aprire una finestra della console in cui è stato compilato il file binario RetryAdo2. exe.  
2. Eseguire RetryAdo2. exe senza parametri di input.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Passaggio 3: modi per testare la logica di ripetizione dei tentativi  
  
Esistono diversi modi per simulare un errore temporaneo per testare la logica di ripetizione dei tentativi.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Passaggio 3. a: generare un'eccezione di test  
  
L'esempio di codice include:  
  
- Una piccola classe secondaria denominata **TestSqlException**con una proprietà denominata **Number**.  
- `//throw new TestSqlException(4060);`, a cui è possibile rimuovere il commento.  
  
Se si rimuove il commento dall'istruzione throw e si ricompila, l'esecuzione successiva di **RetryAdo2. exe** restituisce un risultato simile al seguente.  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Passaggio 3. b: eseguire nuovamente il test con un errore persistente  
  
Per dimostrare che il codice gestisce correttamente gli errori persistenti, eseguire di nuovo il test precedente eccetto non usare il numero di un errore temporaneo reale, ad esempio 4060. Usare invece il numero non sensato 7654321. Il programma deve considerarlo come un errore persistente e deve ignorare eventuali tentativi.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Passaggio 3. c: disconnettersi dalla rete  
  
1. Disconnettere il computer client dalla rete.  
    - Per un desktop, scollegare il cavo di rete.  
    - Per un portatile, premere la funzione combinazione di tasti per disattivare la scheda di rete.  
2. Avviare RetryAdo2. exe e attendere che la console visualizzi il primo errore temporaneo, probabilmente 11001.  
3. Riconnettersi alla rete, mentre RetryAdo2. exe continua a essere eseguito.  
4. Controllare la riuscita della console per un nuovo tentativo.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Passaggio 2. d: digitazione temporanea del nome del server  
  
1. Aggiungere temporaneamente 40615 come numero di errore diverso a **TransientErrorNumbers**e ricompilare.  
2. Impostare un punto di interruzione nella riga `new QC.SqlConnectionStringBuilder()`:.  
3. Usare la funzionalità *modifica e continuazione* per definire in modo errato il nome del server, un paio di righe sotto.  
    - Consentire l'esecuzione del programma e tornare al punto di interruzione.  
    - Si è verificato l'errore 40615.  
4. Correggere l'errore di ortografia.  
5. Consente di eseguire il programma e di completarlo correttamente.  
6. Rimuovere 40615 e ricompilare.  
  
## <a name="next-steps"></a>Next Steps  
  
Per esplorare le procedure consigliate e le linee guida di progettazione, vedere [connessione al database SQL: collegamenti, procedure consigliate e linee guida per la progettazione](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
