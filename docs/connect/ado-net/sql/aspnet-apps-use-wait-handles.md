---
title: Applicazioni ASP.NET tramite handle di attesa
description: Questo documento propone un esempio che spiega come eseguire più comandi simultanei da una pagina ASP.NET, usando gli handle di attesa per gestire l'operazione al completamento di tutti i comandi.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 42d5c395526ff79e24243392bb3dbfa302c8a9e7
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897069"
---
# <a name="aspnet-applications-using-wait-handles"></a>Applicazioni ASP.NET tramite handle di attesa

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

I modelli di callback e di polling per la gestione delle operazioni asincrone sono utili quando l'applicazione elabora solo un'operazione asincrona alla volta. I modelli di attesa offrono un metodo più flessibile per l'elaborazione di più operazioni asincrone. Sono disponibili due modelli di attesa, denominati in base ai metodi <xref:System.Threading.WaitHandle> usati per implementarli: il modello Wait (Any) e il modello Wait (All).  
  
Per usare uno dei due modelli di attesa, è necessario usare la proprietà <xref:System.IAsyncResult.AsyncWaitHandle%2A> dell'oggetto <xref:System.IAsyncResult> restituito dai metodi <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> o <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>. Per i metodi <xref:System.Threading.WaitHandle.WaitAny%2A> e <xref:System.Threading.WaitHandle.WaitAll%2A> è necessario inviare gli oggetti <xref:System.Threading.WaitHandle> come argomento, raggruppati in una matrice.  
  
Entrambi i metodi di attesa monitorano le operazioni asincrone, in attesa del completamento. Il metodo <xref:System.Threading.WaitHandle.WaitAny%2A> consente di attendere il completamento o il timeout di qualsiasi operazione. Quando si apprende che una specifica operazione è stata completata, è possibile elaborarne i risultati e continuare ad attendere il completamento o il timeout dell'operazione successiva. Il metodo <xref:System.Threading.WaitHandle.WaitAll%2A> consente di attendere il completamento o il timeout di tutti i processi nella matrice di istanze <xref:System.Threading.WaitHandle> prima di continuare.  
  
Il vantaggio dei modelli di attesa è più evidente quando è necessario eseguire più operazioni di una certa lunghezza su server diversi o quando il server è abbastanza potente da elaborare tutte le query nello stesso momento. Negli esempi presentati di seguito, tre query emulano processi di lunga durata aggiungendo comandi WAITFOR di lunghezza variabile a query SELECT irrilevanti.  
  
## <a name="example-wait-any-model"></a>Esempio: Modello Wait (Any)  
Nell'esempio seguente è illustrato il modello Wait (Any). Dopo l'avvio di tre processi asincroni, viene chiamato il metodo <xref:System.Threading.WaitHandle.WaitAny%2A> per attendere il completamento di ognuno di essi. Al termine di ogni processo, viene chiamato il metodo <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e viene letto l'oggetto <xref:Microsoft.Data.SqlClient.SqlDataReader> risultante. A questo punto, un'applicazione reale probabilmente userebbe <xref:Microsoft.Data.SqlClient.SqlDataReader> per popolare una parte della pagina. In questo semplice esempio l'ora in cui il processo è stato completato viene aggiunta a una casella di testo corrispondente al processo. Se si osservano assieme, le ore nelle caselle di testo illustrano il punto: Il codice viene eseguito ogni volta che un processo viene completato.  
  
Per impostare questo esempio, creare un nuovo progetto di sito Web ASP.NET. Inserire un controllo <xref:System.Web.UI.WebControls.Button> e quattro controlli <xref:System.Web.UI.WebControls.TextBox> nella pagina, accettando il nome predefinito per ogni controllo.  
  
Aggiungere il codice seguente alla classe del modulo, modificando la stringa di connessione in base alle esigenze dell'ambiente.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,              
     //  you can retrieve it from a configuration file.   
     //  If you have not included "Asynchronous Processing=true"   
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to   
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =   
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous   
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin   
          //  execution. Use the IAsyncResult object returned by   
          //  BeginExecuteReader to add a WaitHandle for the   
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to   
               //  complete. The return value is either the index   
               //  of the array element whose process just   
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,   
                    60000, false);  
               //  This example doesn't actually do anything with   
               //  the data returned by the processes, but the   
               //  code opens readers for each just to demonstrate       
               //  the concept.  
               //  Instead of using the returned data to fill the   
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =   
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =   
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =   
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>Esempio: Modello Wait (All)  
Nell'esempio seguente è illustrato il modello Wait (All). Dopo l'avvio di tre processi asincroni, viene chiamato il metodo <xref:System.Threading.WaitHandle.WaitAll%2A> per attendere il completamento o il timeout dei processi.  
  
Come nell'esempio del modello Wait (Any), l'ora in cui il processo è stato completato viene aggiunta a una casella di testo corrispondente al processo. Nuovamente, le ore nelle caselle di testo illustrano il punto: Il codice che segue il metodo <xref:System.Threading.WaitHandle.WaitAny%2A> viene eseguito solo dopo che tutti i processi vengono completati.  
  
Per impostare questo esempio, creare un nuovo progetto di sito Web ASP.NET. Inserire un controllo <xref:System.Web.UI.WebControls.Button> e quattro controlli <xref:System.Web.UI.WebControls.TextBox> nella pagina, accettando il nome predefinito per ogni controllo.  
  
Aggiungere il codice seguente alla classe del modulo, modificando la stringa di connessione in base alle esigenze dell'ambiente.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,              
    //  you can retrieve it from a configuration file.   
    //  If you have not included "Asynchronous Processing=true"   
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to   
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =   
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous   
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =   
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =   
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin   
        //  execution. Use the IAsyncResult object returned by   
        //  BeginExecuteReader to add a WaitHandle for the   
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to   
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =   
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =   
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =   
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni asincrone](asynchronous-operations.md)
