---
title: 'Passaggio 4: Connettersi in modo resiliente a SQL tramite ADO.NET | Microsoft Docs'
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
manager: jroth
ms.openlocfilehash: b3f7fc6d2d7ab6872bd7100fa51f05a9d9b957c8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770602"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Passaggio 4: Connettersi in modo resiliente a SQL con ADO.NET

- Articolo precedente:&nbsp;&nbsp;&nbsp;[Passaggio 3: Modello di verifica per la connessione a SQL con ADO.NET](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
In questo argomento fornisce un esempio di codice c# che illustra la logica di ripetizione dei tentativi personalizzata. La logica di ripetizione dei tentativi offre affidabilità. La logica di ripetizione dei tentativi è progettata per elaborare correttamente gli errori temporanei o *guasti temporanei* che tendono a risolversi se il programma attende qualche secondo ed i tentativi.  
  
Le origini degli errori temporanei includono:  
  
- Un errore breve della connessione di rete che supporta Internet.  
- Il sistema cloud potrebbe essere il bilanciamento del carico alle relative risorse nel momento in cui che la query è stata inviata.  
  
  
Le classi ADO.NET per la connessione a Microsoft SQL Server locale possono anche connettersi al Database SQL di Azure. Tuttavia, da soli ADO.NET classi non è possibile fornire tutta la solidità e affidabilità necessaria in uso in produzione. Il programma client può incorrere in guasti temporanei da cui deve automaticamente e correttamente ripristinare e continuare a funzionare.  
  
## <a name="step-1-identify-transient-errors"></a>Passaggio 1: Identificare gli errori temporanei  
  
Il programma deve distinguere gli errori temporanei dagli errori persistenti. Gli errori temporanei sono condizioni di errore che potrebbero cancellare entro un breve periodo di tempo, ad esempio problemi di rete temporanei.  Un esempio di un errore permanente durante sarebbe, se il programma presenta un errore di ortografia del nome del database di destinazione: in questo caso, l'errore "Database non trovato" rende persistente e non dispone di alcuna possibilità di la cancellazione dei entro un breve periodo di tempo.  
  
L'elenco dei numeri di errore sono classificati come guasti temporanei è disponibile all'indirizzo [messaggi di errore per le applicazioni client di Database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Passaggio 2: Creare ed eseguire l'applicazione di esempio  
  
In questo esempio si presuppone che .NET Framework 4.5.1 o versione successiva è installato.  L'esempio di codice c# è costituito da un file denominato Program.cs. Il codice viene fornito nella sezione successiva.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Passaggio 2.a: acquisire e compilare il codice di esempio  
  
È possibile compilare l'esempio con i passaggi seguenti:  
  
1. Nel [edizione gratuita Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs), creare un nuovo progetto dal modello di applicazione Console c#.  
    - File > Nuovo > progetto > installati > Modelli > Visual c# > Windows > Desktop classico > applicazione Console  
    - Denominare il progetto **RetryAdo2**.  
2. Aprire il riquadro Esplora soluzioni.  
    - Visualizzare il nome del progetto.  
    - Visualizzare il nome del file Program.cs.  
3. Aprire il file Program.cs.  
4. Sostituire completamente il contenuto del file Program.cs con il codice nel blocco di codice seguente.  
5. Fare clic sul menu compilazione > Compila soluzione.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Passaggio 2: copiare e incollare codice di esempio  
  
Incollare questo codice nelle **Program.cs** file.  
  
È quindi necessario modificare le stringhe per nome del server, password e così via. È possibile trovare queste stringhe nel metodo denominato **GetSqlConnectionStringBuilder**.  
  
Nota: La stringa di connessione per nome del server è rivolto a Database SQL di Azure, poiché include il prefisso di quattro caratteri del **tcp:** . Ma è possibile modificare la stringa di server per connettersi a Microsoft SQL Server.  
  
  
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
  
###  <a name="step-2c-run-the-program"></a>Passaggio 2.c: eseguire il programma  
  
  
Il **RetryAdo2.exe** eseguibile senza parametri di input. Per eseguire il .exe:  
  
1. Aprire una finestra della console per cui è stato compilato il file binario RetryAdo2.exe.  
2. Eseguire RetryAdo2.exe senza parametri di input.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Passaggio 3: Modalità testare la logica di ripetizione dei tentativi  
  
Esistono diversi modi per simulare un errore temporaneo per testare la logica di ripetizione dei tentativi.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Passaggio 3.a: generare un'eccezione di test  
  
Nell'esempio di codice include:  
  
- Una seconda piccola classe denominata **TestSqlException**, con una proprietà denominata **numero**.  
- `//throw new TestSqlException(4060);` , che è possibile rimuovere il commento.  
  
Se si rimuove il commento l'istruzione throw e si ricompila, la successiva esecuzione della **RetryAdo2.exe** restituisce un output simile al seguente.  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Passaggio 3.b: testare nuovamente con un errore persistente  
  
Per verificare se il codice gestisce gli errori persistenti correttamente, eseguire nuovamente il test precedente non usano il numero di un errore temporaneo effettivo, come 4060. Usare invece il numero fittizio 7654321. Il programma deve trattarlo come un errore permanente durante e ignora qualsiasi ripetizione dei tentativi.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Passaggio 3.c: disconnesso dalla rete  
  
1. Disconnettere il computer client dalla rete.  
    - Per un desktop, scollegare il cavo di rete.  
    - In un computer portatile premere la combinazione di tasti per disattivare la scheda di rete in funzione.  
2. Avviare RetryAdo2.exe e attendere che venga visualizzato il primo errore temporaneo, probabilmente il numero 11001.  
3. Ristabilire la connessione alla rete mentre RetryAdo2.exe è ancora in esecuzione.  
4. Guarda il successo di report di console in un tentativo successivo.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Passaggio 2.d: temporaneamente in modo errato il nome del server  
  
1. Aggiunta temporanea di come un altro numero di errore 40615 **TransientErrorNumbers**e ricompilare.  
2. Impostare un punto di interruzione sulla riga: `new QC.SqlConnectionStringBuilder()`.  
3. Usare la *modifica e continuazione* intenzionalmente in modo errato il nome del server, un paio di righe più in basso della funzionalità.  
    - Consentire il programma eseguito ed è tornato al punto di interruzione.  
    - Si verifica l'errore 40615.  
4. Correggere l'errore di ortografia.  
5. Consentire il programma eseguite e completate correttamente.  
6. Rimuovere il numero 40615 e ricompilare.  
  
## <a name="next-steps"></a>Next Steps  
  
Per esplorare altri practicies procedure e linee guida di progettazione, visitare [la connessione al Database SQL: collegamenti, procedure consigliate e linee guida di progettazione](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
