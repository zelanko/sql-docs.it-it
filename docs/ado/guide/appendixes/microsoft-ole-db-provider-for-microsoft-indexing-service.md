---
title: Provider Microsoft OLE DB per il servizio di indicizzazione Microsoft | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5a81514fd12117a9f43e2c33bf0cda579fb363d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926668"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Panoramica di Microsoft OLE DB provider per il servizio di indicizzazione Microsoft
Il provider Microsoft OLE DB per Microsoft Indexing Service fornisce l'accesso di sola lettura a livello di codice ai file system e ai dati web indicizzati dal servizio Microsoft Indexing. Le applicazioni ADO possono eseguire query SQL per recuperare il contenuto e le informazioni sulle proprietà del file.

 Il provider è a thread libero e il formato UNICODE è abilitato.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare l'argomento **provider =** sulla proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) su:

```vb
MSIDXS
```

 La lettura della proprietà del [provider](../../../ado/reference/ado-api/provider-property-ado.md) restituirà anche questa stringa.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è la seguente:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 La stringa è costituita dalle parole chiave seguenti:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il provider di OLE DB per il servizio di indicizzazione Microsoft. Si tratta in genere dell'unica parola chiave specificata nella stringa di connessione.|
|**Origine dati**|Specifica il nome del catalogo del servizio di indicizzazione. Se questa parola chiave non è specificata, viene utilizzato il catalogo di sistema predefinito.|
|**Locale Identifier**|Specifica un numero univoco a 32 bit (ad esempio, 1033) che specifica le preferenze relative alla lingua dell'utente. Se questa parola chiave non è specificata, viene utilizzato l'identificatore delle impostazioni locali di sistema predefinito.|

## <a name="command-text"></a>Testo comando
 La sintassi di query SQL del servizio di indicizzazione è costituita dalle estensioni all'istruzione SQL-92 **Select** e dalle clausole **from** e **where** . I risultati della query vengono restituiti tramite OLE DB set di righe, che possono essere utilizzati da ADO e modificati come oggetti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .

 È possibile cercare parole o frasi esatte oppure usare caratteri jolly per cercare modelli o steli di parole. La logica di ricerca può essere basata su decisioni booleane, termini ponderati o prossimità ad altre parole. È anche possibile eseguire la ricerca per "testo libero", che trova le corrispondenze in base al significato, anziché a parole esatte.

 Il dialetto del comando specifico è completamente documentato nella documentazione relativa ai linguaggi di query per l'indicizzazione del servizio.

 Il provider non accetta stored procedure chiamate o nomi di tabella semplici (ad esempio, la proprietà [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) sarà sempre **adCmdText**).

## <a name="recordset-behavior"></a>Comportamento del recordset
 Nelle tabelle seguenti sono elencate le funzionalità disponibili con un oggetto **Recordset** aperto con questo provider. È disponibile solo il tipo di cursore statico (**adOpenStatic**).

 Per informazioni più dettagliate sul comportamento del **Recordset** per la configurazione del provider, eseguire il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) ed enumerare la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) del **Recordset** per determinare se sono presenti proprietà dinamiche specifiche del provider.

 **Disponibilità delle proprietà del recordset ADO standard:**

|Proprietà|Disponibilità|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lettura/scrittura|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lettura/scrittura|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Sola lettura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|
|[Segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)*|lettura/scrittura|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lettura/scrittura|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|sempre **adUseServer come**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|sempre **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lettura/scrittura|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lettura/scrittura|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|non disponibile|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lettura/scrittura|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Sola lettura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lettura/scrittura|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Sola lettura|
|[origine](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lettura/scrittura|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|Sola lettura|
|[Stato](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Sola lettura|

 \*I segnalibri devono essere abilitati nel provider affinché questa funzionalità sia presente nel **Recordset**.

 **Disponibilità dei metodi Recordset ADO standard:**

|Metodo|Disponibile?|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|No|
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|Sì|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md) (Clona)|Sì|
|[Chiudi](../../../ado/reference/ado-api/close-method-ado.md)|Sì|
|[Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sì|
|[Spostamento](../../../ado/reference/ado-api/move-method-ado.md)|Sì|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sì|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sì|
|[Apri](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sì|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sì|
|[Risincronizza](../../../ado/reference/ado-api/resync-method.md)|Sì|
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Sì|
|[Aggiornamento](../../../ado/reference/ado-api/update-method.md)|No|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|

 Per informazioni dettagliate sull'implementazione e informazioni funzionali sul provider Microsoft OLE DB per Microsoft Indexing Service, consultare la [Guida per programmatori OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)oppure visitare la pagina dei servizi Web del sito Web Windows NT Server.

## <a name="see-also"></a>Vedere anche
 Proprietà [CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [CONNECTIONSTRING Property (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Properties collection](../../../ado/reference/ado-api/properties-collection-ado.md) (ADO) [provider Property](../../../ado/reference/ado-api/provider-property-ado.md) (ADO) [Recordset Object (](../../../ado/reference/ado-api/recordset-object-ado.md) ADO) supporta il [Metodo](../../../ado/reference/ado-api/supports-method.md)
