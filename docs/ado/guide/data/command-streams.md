---
title: Comando flussi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd0c2273739a3651c7fdd4c424ce0cb47d39dd5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925848"
---
# <a name="command-streams"></a>Flussi di comandi
ADO ha sempre supportato l'input del comando nel formato di stringa specificato tramite il **CommandText** proprietà. In alternativa, con ADO 2.7 o versione successiva, è possibile anche usare un flusso di informazioni per l'input comando tramite l'assegnazione di flusso in cui il **CommandStream** proprietà. È possibile assegnare un oggetto ADO **Stream** oppure qualsiasi oggetto che supporta il modello COM **IStream** interfaccia.  
  
 Il contenuto del flusso del comando viene semplicemente passato da ADO per il provider, in modo che il provider deve supportare l'input del comando dal flusso per usare questa funzionalità. Ad esempio, SQL Server supporta le query sotto forma di modelli XML o estensioni di OpenXML per Transact-SQL.  
  
 Poiché i dettagli del flusso devono essere interpretati dal provider, è necessario specificare il sottolinguaggio del comando impostando il **sottolinguaggio** proprietà. Il valore di **sottolinguaggio** è una stringa contenente un GUID, che viene definito dal provider. Per informazioni sui valori validi per **sottolinguaggio** supportato dal provider, vedere la documentazione del provider.  
  
## <a name="xml-template-query-example"></a>Esempio di Query modello XML  
 Nell'esempio seguente viene scritto in VBScript al database Northwind.  
  
 In primo luogo, inizializzare e aprire il **Stream** oggetto che verrà usato per contenere il flusso di query:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 Il contenuto del flusso di query sarà una query del modello XML.  
  
 La query del modello richiede un riferimento allo spazio dei nomi XML identificato da sql: prefisso di \<SQL: query > tag. Un'istruzione SQL SELECT è incluso il contenuto del modello XML e assegnata a una variabile di stringa, come indicato di seguito:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 Successivamente, scrivere la stringa nel flusso:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 Assegnare adoStreamQuery per il **CommandStream** proprietà di un oggetto ADO **comando** oggetto:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Specificare il linguaggio di comando **sottolinguaggio**, che indica come il Provider OLE DB di SQL Server devono interpretare il flusso del comando. Il dialetto specificato da un GUID specifico del provider:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Infine, eseguire la query e restituire i risultati in un **Recordset** oggetto:  
  
```  
Set objRS = adoCmd.Execute  
```
