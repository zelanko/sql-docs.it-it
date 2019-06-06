---
title: Provider Microsoft OLE DB per Microsoft Indexing Service | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: dea7ec95efc1f560a2279868b2116d02d7ad6fef
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701210"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Provider Microsoft OLE DB per Microsoft Panoramica del servizio di indicizzazione
Il Provider Microsoft OLE DB per Microsoft Indexing Service fornisce l'accesso di sola lettura a livello di codice per file system e i dati Web indicizzati dal servizio di indicizzazione Microsoft. Le applicazioni ADO possono eseguire query SQL per recuperare le informazioni sulle proprietà di contenuto e file.

 Il provider è a thread libero e abilitata per UNICODE.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare il **Provider =** argomento per il [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà:

```vb
MSIDXS
```

 Leggere il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà restituirà anche questa stringa.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il Provider OLE DB per Microsoft Indexing Service. In genere questo è l'unica parola chiave specificata nella stringa di connessione.|
|**Data Source**|Specifica il nome del catalogo del servizio di indicizzazione. Se questa parola chiave non viene specificata, viene utilizzato il catalogo di sistema predefinito.|
|**Locale Identifier**|Specifica un numero a 32 bit univoco (ad esempio, 1033) che specifica le preferenze relative alla lingua dell'utente. Se questa parola chiave non viene specificata, viene usato l'identificatore delle impostazioni locali del sistema predefinito.|

## <a name="command-text"></a>Testo comando
 La sintassi di query SQL del servizio di indicizzazione è costituito da estensioni per il SQL-92 **selezionate** istruzione e il relativo **FROM** e **dove** clausole. I risultati della query vengono restituiti tramite set di righe OLE DB, che possono essere utilizzate da ADO e modificati come [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti.

 È possibile cercare parole o frasi esatte o usare caratteri jolly per eseguire la ricerca di radici di parole o modelli. Logica di ricerca può basarsi su prossimità in altre parole, termini ponderati o decisioni booleane. È anche possibile cercare "testo libero", che consente di trovare corrispondenze basate su significato, anziché termini esatti.

 Il sottolinguaggio del comando specifico è completamente documentato in linguaggi di Query per la documentazione del servizio di indicizzazione.

 Il provider non accetta chiamate di stored procedure o i nomi di tabella semplice (ad esempio, il [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) proprietà sarà sempre **adCmdText**).

## <a name="recordset-behavior"></a>Comportamento dell'oggetto Recordset
 Le tabelle seguenti elencano le funzionalità disponibili con un **Recordset** aprire l'oggetto con questo provider. Solo il tipo di cursore statico (**adOpenStatic**) è disponibile.

 Per informazioni più dettagliate sui **Recordset** comportamento per la configurazione del provider, eseguire il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo ed enumerare il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta del **Recordset** per determinare se sono presenti proprietà dinamiche specifiche del provider.

 **Disponibilità di proprietà Recordset ADO standard:**

|Proprietà|Disponibilità|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lettura/scrittura|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lettura/scrittura|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Sola lettura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|
|[Segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)*|lettura/scrittura|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lettura/scrittura|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lettura/scrittura|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lettura/scrittura|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|non disponibile|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lettura/scrittura|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Sola lettura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lettura/scrittura|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Sola lettura|
|[Origine](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lettura/scrittura|
|[Stato](../../../ado/reference/ado-api/state-property-ado.md)|Sola lettura|
|[Stato](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Sola lettura|

 \*I segnalibri è necessario attivare il provider per questa funzionalità esiste nel **Recordset**.

 **Disponibilità di metodi di Recordset ADO standard:**

|Metodo|Disponibile?|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|No|
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|Yes|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Yes|
|[Chiudi](../../../ado/reference/ado-api/close-method-ado.md)|Yes|
|[Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Yes|
|[Sposta](../../../ado/reference/ado-api/move-method-ado.md)|Yes|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Yes|
|[Aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Yes|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Yes|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Yes|
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Yes|
|[Update](../../../ado/reference/ado-api/update-method.md)|No|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|

 Per dettagli specifici sull'implementazione e informazioni funzionale su Provider Microsoft OLE DB per Microsoft Indexing Service, consultare il [Guida per programmatori OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx), oppure visitare la pagina servizi Web di Windows NT Server Web sito.

## <a name="see-also"></a>Vedere anche
 [Proprietà CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [proprietà Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [ Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [supporta (metodo)](../../../ado/reference/ado-api/supports-method.md)
