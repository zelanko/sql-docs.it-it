---
title: Esecuzione di query SQL (classi gestite SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXML Managed Classes
- SQLXML Managed Classes, executing SQL queries
- Managed Classes [SQLXML], executing SQL queries
- ExecuteToStream method
- SQL queries [SQLXML]
ms.assetid: a561ae83-a8b6-4b9b-a819-9b86839546b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f8e16ff3651b9ce23fafe99137b4905eb3961ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014934"
---
# <a name="executing-sql-queries-sqlxml-managed-classes"></a>Esecuzione di query SQL (classi gestite SQLXML)
  In questo esempio vengono illustrate le operazioni seguenti:  
  
-   Creazione di parametri (oggetti SqlXmlParameter).  
  
-   Assegnazione di valori alle proprietà (nome e valore) degli oggetti SqlXmlParameter.  
  
 In questo esempio viene eseguita una query SQL semplice per recuperare il nome, il cognome e la data di nascita del dipendente il cui valore di cognome viene passato come parametro. Quando si specifica il parametro (*LastName*), viene impostata solo la proprietà Value. La proprietà Name non è impostata perché in questa query il parametro è posizionale e non è necessario alcun nome.  
  
 Per impostazione predefinita, la proprietà CommandType dell'oggetto SqlXmlCommand è **SQL**. La proprietà, pertanto, non viene impostata in modo esplicito.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione.  
  
 Di seguito viene fornito il codice C#:  
  
```  
using System;  
  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);        
         cmd.CommandText = "SELECT FirstName, LastName FROM Person.Contact WHERE LastName=? For XML Auto";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         string strResult;  
         try   
         {  
            strm = cmd.ExecuteStream();  
            strm.Position = 0;  
            using(StreamReader sr = new StreamReader(strm))  
            {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         catch (SqlXmlException e)  
         {  
            //in case of an error, this prints error returned.  
            e.ErrorStream.Position=0;  
            strResult=new StreamReader(e.ErrorStream).ReadToEnd();  
            System.Console.WriteLine(strResult);  
         }  
  
         return 0;  
   }  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
### <a name="to-test-the-application"></a>Per testare l'applicazione  
  
1.  Salvare in una cartella il codice C# (DocSample.cs) fornito in questo argomento.  
  
2.  Compilare il codice. Per compilare il codice al prompt dei comandi, utilizzare:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Viene creato un file eseguibile (DocSample.exe).  
  
3.  Al prompt dei comandi eseguire DocSample.exe.  
  
 Per testare questo esempio, è necessario che nel computer sia installato [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework.  
  
 Anziché specificare query SQL come testo del comando, è possibile specificare un modello, come illustrato nel frammento di codice seguente, che esegua un updategram (che è anche un modello) per inserire un record del consumer. È possibile specificare modelli e updategram in file e file di esecuzione. Per ulteriori informazioni, vedere [esecuzione di file modello tramite la proprietà CommandText](executing-template-files-by-using-the-commandtext-property.md).  
  
```  
SqlXmlCommand cmd = new SqlXmlCommand("Provider=SQLOLEDB;Data Source=SqlServerName;Initial Catalog=Database; Integrated Security=SSPI;");  
Stream stm;  
cmd.CommandType = SqlXmlCommandType.UpdateGram;  
cmd.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' xmlns:updg='urn:schemas-microsoft-com:xml-updategram'>" +  
      "<updg:sync>" +  
       "<updg:before/>" +  
       "<updg:after>" +  
         "<Customer CustomerID='aaaaa' CustomerName='Some Name' CustomerTitle='SomeTitle' />" +  
       "</updg:after>" +  
       "</updg:sync>" +  
       "</ROOT>";  
  
stm = cmd.ExecuteStream();  
stm = null;  
cmd = null;  
```  
  
## <a name="using-executetostream"></a>Utilizzo di ExecuteToStream  
 Se si dispone di un flusso esistente, è possibile usare il metodo ExecuteToStream anziché creare un oggetto flusso e usare il metodo Execute. Il codice dell'esempio precedente è stato modificato qui per usare il metodo ExecuteToStream:  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlParameter p;  
      MemoryStream ms = new MemoryStream();  
      StreamReader sr = new StreamReader(ms);  
      ms.Position = 0;  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.CommandText = "select FirstName, LastName from Person.Contact where LastName = ? For XML Auto";  
      p = cmd.CreateParameter();  
      p.Value = "Achong";  
      cmd.ExecuteToStream(ms);  
      ms.Position = 0;  
      Console.WriteLine(sr.ReadToEnd());  
      return 0;        
   }  
   public static int Main(String[] args)  
   {  
      testParams();     
      return 0;  
   }  
}  
```  
  
> [!NOTE]  
>  È anche possibile usare ExecuteXMLReadermethod che restituisce un oggetto XmlReader. Per ulteriori informazioni, vedere [esecuzione di query SQL tramite il metodo ExecuteXmlReader](executing-sql-queries-by-using-the-executexmlreader-method.md).  
  
  
