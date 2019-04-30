---
title: Esecuzione di un DiffGram mediante ADO (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 302136888fe562161c6399a9ba75c50429e301ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127746"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>Esecuzione di un DiffGram mediante ADO (SQLXML 4.0)
  Questa applicazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic utilizza ADO per stabilire una connessione a un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quindi esegue un DiffGram. In questa applicazione il DiffGram e lo schema XSD vengono archiviati in un file. L'applicazione carica il DiffGram dal file specificato. È possibile usare uno dei DiffGram (e lo schema XSD associato) descritto nella [esempi di DiffGram](diffgram-examples-sqlxml-4-0.md).  
  
 Il processo per l'applicazione di esempio è il seguente:  
  
-   Il **conn** oggetto (**ADODB. Connessione**) stabilisce una connessione a un'istanza di SQL Server in esecuzione in un server specifico.  
  
-   Il **cmd** oggetto (**ADODB. Command**) viene eseguito durante la connessione.  
  
-   Il sottolinguaggio del comando viene impostato su DBGUID_MSSQLXML.  
  
-   Il DiffGram viene copiato nel flusso di comandi (**strmIn**) da un file.  
  
-   Flusso di output del comando è impostato il **StrmOut** oggetto (**ADODB. Stream**) per ricevere eventuali dati restituiti.  
  
-   Quando si utilizza il provider SQLOLEDB, per impostazione predefinita si otterrà la funzionalità Microsoft SQLXML fornita da Sqlxmlx.dll. Per utilizzare Sqlxml4.dll con il Provider SQLOLEDB, il **SQLXML Version** proprietà deve essere impostata su **SQLXML.4.0** il provider SQLOLEDB **connessione** oggetto.  
  
-   Il comando (DiffGram) viene eseguito.  
  
 Di seguito viene riportato il codice dell'applicazione di esempio:  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione.  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>Per testare DiffGram  
  
1.  In una cartella nel computer, copiare uno dei DiffGram e lo schema XSD corrispondente da uno degli esempi nella [esempi di DiffGram](diffgram-examples-sqlxml-4-0.md).  
  
2.  Aprire Visual Basic e creare un progetto Standard Exe.  
  
3.  Aggiungere i riferimenti seguenti al progetto:  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  Nella casella degli strumenti, fare clic su **CommandButton**, quindi disegnare un pulsante nel form.  
  
5.  Fare doppio clic sul pulsante per modificare il codice e aggiungere il codice dell'applicazione fornito nell'argomento.  
  
6.  Modificare il codice per specificare i nomi dei file DiffGram e XSD. Modificare anche la stringa di connessione in modo appropriato.  
  
7.  Eseguire l'applicazione. Il risultato dell'esecuzione dipende dal DiffGram che si esegue.  
  
  
