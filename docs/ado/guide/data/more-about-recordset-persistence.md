---
title: Ulteriori informazioni sulla persistenza dei recordset | Microsoft Docs
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
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bee7d185d5f598a2f0a086bb7e3bea49ddfff88c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924903"
---
# <a name="more-about-recordset-persistence"></a>Altre informazioni sulla persistenza dei recordset
L'oggetto recordset ADO supporta l'archiviazione del contenuto di un oggetto **Recordset** in un file tramite il relativo metodo [Save](../../../ado/reference/ado-api/save-method.md) . Il file archiviato in modo permanente può esistere in un'unità locale, in un server o come URL in un sito Web. Successivamente, il file può essere ripristinato con il metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) dell'oggetto **Recordset** o il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) dell'oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
 Inoltre, il metodo [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) converte un oggetto **Recordset** in un modulo in cui le colonne e le righe sono delimitate da caratteri specificati dall'utente.  
  
 Per salvare in modo permanente un **Recordset**, iniziare con la conversione in un modulo che può essere archiviato in un file. Gli oggetti **Recordset** possono essere archiviati nel formato ADTG (Advanced Data TableGram) proprietario o nel formato Open Extensible Markup Language (XML). Gli esempi di ADTG sono illustrati nella sezione successiva. Per ulteriori informazioni sulla persistenza XML, vedere [persistenza dei record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Salvare tutte le modifiche in sospeso nel file permanente. In questo modo è possibile eseguire una query che restituisce un oggetto **Recordset** , modificare il **Recordset**, salvarlo e le modifiche in sospeso, successivamente ripristinare il **Recordset**, quindi aggiornare l'origine dati con le modifiche in sospeso salvate.  
  
 Per informazioni sull'archiviazione persistente di oggetti di **flusso** , vedere [flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md).  
  
 Per un esempio di persistenza dei **Recordset** , vedere lo scenario di persistenza dei recordset XML.  
  
## <a name="example"></a>Esempio  
  
### <a name="save-a-recordset"></a>Salvare un recordset:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Aprire un file permanente con recordset. Open:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 Facoltativamente, se il **Recordset** non dispone di una connessione attiva, è possibile accettare tutte le impostazioni predefinite e scrivere il codice seguente:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Aprire un file permanente con Connection. Execute:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Aprire un file permanente con Servizi Desktop remoto. DataControl  
 In questo caso, la proprietà **Server** non è impostata.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Provider di persistenza Microsoft OLE DB (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md)
