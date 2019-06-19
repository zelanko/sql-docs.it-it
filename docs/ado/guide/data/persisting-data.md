---
title: Rendere persistenti i dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f2d47229b7383c11740ca3d7a20ad8e420931a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700479"
---
# <a name="persisting-data"></a>Persistenza dei dati
Computer portatili (ad esempio, Usa computer portatili) ha generato l'esigenza di applicazioni eseguibili in uno stato connesso e disconnesso. ADO ha aggiunto il supporto per l'oggetto da fornire allo sviluppatore la possibilità di salvare un cursore sul lato client **Recordset** su disco e caricarla in un secondo momento.  
  
 Esistono diversi scenari in cui è possibile usare questo tipo di funzionalità, incluse le seguenti:  
  
-   **In viaggio:** Quando si esegue l'applicazione in viaggio, è essenziale per fornire la possibilità di apportare modifiche e aggiungere nuovi record che possono essere riconnesse al database in un secondo momento e il commit.  
  
-   **Ricerche vengono aggiornate raramente:** In un'applicazione, le tabelle vengono spesso utilizzate come le ricerche, ad esempio stato tabelle imposta sulle vendite. Che vengono aggiornati di rado e sono di sola lettura. Invece di rileggere i dati dal server ogni volta che l'applicazione viene avviata, l'applicazione può caricare semplicemente i dati da un locale persistente **Recordset**.  
  
 In ADO, salvare e caricare **recordset**, utilizzare il **Recordset. Save** e **Recordset.Open(,,,adCmdFile)** metodi sull'oggetto ADO **Recordset**oggetto.  
  
 È possibile usare la **Recordset salvataggio** metodo per rendere persistenti i ADO **Recordset** in un file su disco. (È anche possibile salvare una **Recordset** a un oggetto ADO **Stream** oggetto. **Stream** gli oggetti sono descritti più avanti nella Guida.) In un secondo momento, è possibile usare la **aperto** metodo per riaprire il **Recordset** quando è pronti a usarlo. Per impostazione predefinita, ADO Salva il **Recordset** nel formato proprietario Microsoft avanzata dei dati viene (ADTG). Questo formato binario viene specificato usando il **adPersistADTG PersistFormatEnum** valore. In alternativa, è possibile scegliere di salvare il **Recordset** out come XML usando invece **il valore adPersistXML**. Per altre informazioni sul salvataggio di recordset in formato XML, vedere [record di persistenza in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 La sintassi del **salvare** è la seguente:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 La prima volta che salva il **Recordset**, è possibile specificare facoltativamente *destinazione*. Se si omette *destinazione*, verrà creato un nuovo file con un nome impostato sul valore della [origine](../../../ado/reference/ado-api/source-property-ado-recordset.md) proprietà del **Recordset**.  
  
 Omettere *destinazione* quando si chiama successivamente **salvare** dopo il primo salvataggio o un errore di run-time si verificherà. Se successivamente si chiama **salvare** con un nuovo oggetto *destinazione*, il **Recordset** viene salvato nella nuova destinazione. Tuttavia, la nuova destinazione e la destinazione originale entrambi saranno aperte.  
  
 **Salvare** non chiude il **Recordset** o *destinazione*, quindi è possibile continuare a lavorare con i **Recordset** e salvare le modifiche più recenti. *Destinazione* rimane aperta fino a quando il **Recordset** viene chiusa, durante i quali altre applicazioni possono leggere ma non di scrivere *destinazione*.  
  
 Per motivi di sicurezza, il **salvare** metodo consente solo l'uso delle impostazioni di sicurezza personalizzato e basso da uno script eseguito da Microsoft Internet Explorer.  
  
 Se il **salvare** viene chiamato durante un'asincrona **Recordset** recuperare, eseguire o aggiornare è in corso l'operazione **Salva** attende fino a quando l'operazione asincrona è completare.  
  
 Vengono salvati i record che iniziano con la prima riga del **Recordset**. Quando la **salvare** metodo termina, la posizione della riga corrente viene spostata sulla prima riga del **Recordset**.  
  
 Per ottenere risultati ottimali, impostare il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient** con **Salva**. Se il provider non supporta tutte le funzionalità necessarie per salvare **Recordset** oggetti, il servizio di cursore fornirà tale funzionalità.  
  
 Quando un **Recordset** persistente con il **CursorLocation** proprietà impostata su **adUseServer**, la funzionalità di aggiornamento per il **Recordset**è limitato. In genere, solo tabella singola aggiornamenti, inserimenti ed eliminazioni sono consentite (dipende da funzionalità del provider). Il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo è anche disponibile in questa configurazione.  
  
 Poiché il *destinazione* parametro può accettare qualsiasi oggetto che supporta OLE DB **IStream** interfaccia, è possibile salvare una **Recordset** direttamente a ASP  **Risposta** oggetto.  
  
 Nell'esempio seguente, il **salvare** e **Open** vengono utilizzati metodi per rendere persistente un **Recordset** e riaprirlo successivamente:  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Note  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Altre informazioni sulla persistenza dei recordset](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Persistenza di recordset filtrati e gerarchici](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
