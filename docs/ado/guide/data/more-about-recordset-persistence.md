---
title: Ulteriori informazioni sulla persistenza dei Recordset | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3e626c924e7b84312877b47f811329e215f47e42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161588"
---
# <a name="more-about-recordset-persistence"></a>Altre informazioni sulla persistenza dei recordset
L'oggetto Recordset ADO supporta la memorizzazione di contenuto di un **Recordset** oggetto in un file con relativo [salvare](../../../ado/reference/ado-api/save-method.md) (metodo). Il file salvato in modo permanente possono essere presenti in locale l'unità e server, o come un URL in una pagina Web del sito. In un secondo momento, il file può essere ripristinato con il [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo per il **Recordset** oggetto o il [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) metodo del [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
 Inoltre, il [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) metodo converte una **Recordset** oggetto a un form in cui le righe e colonne sono delimitate con caratteri specificati dall'utente.  
  
 Per rendere persistente un **Recordset**, iniziare è necessario convertirlo in un form che può essere archiviato in un file. **Recordset** gli oggetti possono essere archiviati nel formato avanzata dei dati viene (ADTG) proprietarie o open formato Extensible Markup Language (XML). Esempi ADTG vengono visualizzati nella sezione successiva. Per altre informazioni sulla persistenza di XML, vedere [record di persistenza in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Salvare le modifiche in sospeso in file persistente. Questa operazione consente di inviare una query che restituisce un **Recordset** (oggetto), le modifiche le **Recordset**, Salva le modifiche in sospeso, in seguito ripristina il **Recordset**e quindi Aggiorna l'origine dati con il salvato le modifiche in sospeso.  
  
 Per informazioni sulla memorizzazione persistente **Stream** oggetti, vedere [flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md).  
  
 Per un esempio di **Recordset** persistenza, vedere lo Scenario di persistenza Recordset XML.  
  
## <a name="example"></a>Esempio  
  
### <a name="save-a-recordset"></a>Salvare un set di record:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Aprire un file persistente con Open:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 Facoltativamente, se il **Recordset** viene non dispone di una connessione attiva, è possibile accettare tutte le impostazioni predefinite e di codice seguente:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Aprire un file persistente con Connection:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Aprire un file persistente con Servizi Desktop remoto. DataControl:  
 In questo caso, il **Server** proprietà non è impostata.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Provider di persistenza Microsoft OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md)
