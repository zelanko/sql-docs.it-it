---
title: Utilizzare ADO per SQLXML 4.0 di eseguire una query | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2a8f5cdb74385852a0feef0f9de0d760eb57f13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012152"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>Utilizzo di ADO per eseguire query SQLXML 4.0
  Nelle versioni precedenti di SQLXML viene fornito il supporto per l'esecuzione di query basate su HTTP mediante le directory virtuali IIS e il filtro ISAPI SQLXML. In SQLXML 4.0 questi componenti sono stati rimossi in quanto simili e, a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è stata fornita una funzionalità sostitutiva con i servizi Web XML nativi.  
  
 In alternativa, è possibile eseguire query e utilizzare SQLXML 4.0 con le applicazioni basate su COM sfruttando le estensioni SQLXML di ActiveX Data Objects (ADO), introdotte per la prima volta in Microsoft Data Access Components (MDAC) 2.6 e versioni successive.  
  
 In questo argomento viene illustrato l'utilizzo di SQLXML e ADO come parte di un'applicazione Visual Basic, Scripting Edition (VBScript), ovvero di un file di script con estensione vbs. Vengono illustrate le procedure di configurazione iniziale per consentire di ricreare e testare gli esempi di query forniti nella documentazione di SQLXML 4.0.  
  
## <a name="creating-the-sqlxml-40-test-script"></a>Creazione dello script di test di SQLXML 4.0  
 In questa procedura viene creato un file VBScript con estensione vbs, ovvero Sqlxml4test.vbs, che può essere utilizzato per eseguire query SQLXML sfruttando le estensioni ADO di SQLXML in ADO 2.6 e versioni successive.  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>Per creare il file di test della query SQLXML 4.0 utilizzando ADO (VBScript).  
  
1.  Copiare il codice seguente e incollarlo in un file di testo: Salvare il file come Sqlxml4test.vbs.  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  Aggiornare i valori dello script seguenti per l'esempio che si sta tentando di testare e l'ambiente di prova.  
  
    -   Trovare "`@@FILE_NAME@@`" e sostituirlo con il nome del file modello.  
  
    -   Trovare "`@@SERVER_NAME@@`" e sostituirlo con il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ad esempio, "`(local)`" se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in locale).  
  
    -   Trovare "`@@DATABASE_NAME@@`" e sostituirlo con il nome del database (ad esempio "`AdventureWorks2012`" o "`tempdb`").  
  
     Aggiornare gli altri valori se menzionato nelle istruzioni specifiche per l'esempio che si sta tentando di ricreare in locale nel computer.  
  
3.  Salvare il file e chiuderlo.  
  
4.  Verificare la creazione di eventuali file aggiuntivi, ad esempio schemi o modelli XML che fanno parte dell'esempio che si sta tentando di ricreare in locale nel computer. Questi file devono trovarsi nella stessa directory in cui è stato salvato il file dello script di test (Sqlxml4test.vbs).  
  
5.  Seguire le istruzioni riportate nella sezione successiva per informazioni sull'utilizzo dello script di test SQLXML 4.0.  
  
## <a name="using-the-sqlxml-40-test-script"></a>Utilizzo dello script di test di SQLXML 4.0  
 Nella procedura seguente viene illustrato come utilizzare i file Sqlxml4test.vbs per testare le query di esempio fornite in questa documentazione.  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>Per utilizzare il file di test della query SQLXML 4.0  
  
1.  Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sia installato, come segue:  
  
    1.  Dal **Start** dal menu **impostazioni**, quindi fare clic su **Pannello di controllo**.  
  
    2.  Nel Pannello di controllo aprire **Installazione applicazioni**  
  
    3.  Nell'elenco dei programmi attualmente installati, verificare che **Microsoft SQL Server Native Client** viene visualizzato nell'elenco.  
  
        > [!NOTE]  
        >  Se è necessario installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vedere [installazione di SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
2.  Verificare che la versione di MDAC installata per il computer client sia 2.6 o successiva. Se è necessario verificare le informazioni sulla versione di MDAC, è possibile utilizzare lo strumento MDAC Component Checker fornito come download gratuito dal sito Web Microsoft (www.microsoft.com). Per ulteriori informazioni, cercare "MDAC Component Checker" sul sito Web Microsoft.  
  
3.  Eseguire lo script.  
  
     È possibile eseguire il file VBScript alla riga di comando utilizzando Cscript.exe o facendo doppio clic sul file Sqlxml4test.vbs per richiamare Windows Script Host (WScript.exe).  
  
     Quando viene eseguito, lo script visualizza un messaggio per avvisare che l'esecuzione potrebbe richiedere tempo prima che vengano restituiti e visualizzati i risultati della query come output dello script. Una volta visualizzato l'output, confrontarne il contenuto con i risultati previsti per l'esempio.  
  
  
