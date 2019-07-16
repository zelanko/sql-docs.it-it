---
title: Microsoft Cursor Service per OLE DB (ADO componente del servizio) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7e5b9a973e5ccf04f92a2162d88ee25b7fa5242
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926790"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Microsoft Cursor Service per OLE DB Panoramica
Il Microsoft Cursor Service per OLE DB integrano le funzioni di supporto del cursore del provider di dati. Di conseguenza, l'utente percepisce funzionalità relativamente uniforme di tutti i provider di dati.

 Il servizio di cursore rende disponibili le proprietà dinamiche e migliora il comportamento di determinati metodi. Ad esempio, il [Ottimizza](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) proprietà dinamica consente la creazione di indici temporanei per rendere alcune operazioni, ad esempio le [trovare](../../../ado/reference/ado-api/find-method-ado.md) (metodo).

 Il servizio di cursore Abilita il supporto per l'aggiornamento in batch in tutti i casi. Simula anche in grado di supportare più tipi di cursore, ad esempio i cursori dynamic, quando un provider di dati possa fornire solo i cursori meno efficienti, ad esempio i cursori statici.

## <a name="keyword"></a>Parola chiave
 Per richiamare questo componente del servizio, impostare il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oppure [connessione](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Quando viene richiamato il Cursor Service per OLE DB, le seguenti proprietà dinamiche vengono aggiunti per il **Recordset** dell'oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta. L'elenco completo dei **Connection** e **Recordset** le proprietà dell'oggetto dinamico è elencato nella [indice proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). I nomi di proprietà OLE DB associati, dove appropriato, sono inclusi tra parentesi dopo il nome della proprietà ADO.

 Dopo aver richiamato il servizio di cursore, le modifiche apportate ad alcune proprietà dinamica non sono visibili all'origine dati sottostante. Ad esempio, impostando il *timeout del comando* proprietà in un **Recordset** non sarà visibile al provider di dati sottostante.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Se l'applicazione richiede che il servizio di cursore, ma è necessario impostare le proprietà dinamiche per il provider sottostante, impostare le proprietà prima di richiamare il servizio di cursore. Le impostazioni delle proprietà di oggetto comando vengono sempre passati al provider di dati sottostante, indipendentemente dalla posizione del cursore. Pertanto, è possibile utilizzare anche un oggetto comando per impostare le proprietà in qualsiasi momento.

> [!NOTE]
>  La proprietà dinamica DBPROP_SERVERDATAONINSERT non è supportata dal servizio di cursore, anche se è supportata dal provider di dati sottostante.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|Ricalcolo automatico (DBPROP_ADC_AUTORECALC)|Per i recordset creato con il Data shaping, questo valore indica quanto spesso vengono calcolate le colonne calcolate e di aggregazione. Il valore predefinito (valore = 1) consiste nel ricalcolare ogni volta che il Data Shaping determina che i valori sono stati modificati. Se il valore è 0, le colonne calcolate o aggregate vengono calcolate solo quando la gerarchia viene creata inizialmente.|
|Dimensioni del batch (DBPROP_ADC_BATCHSIZE)|Indica il numero di istruzioni update che possono essere raggruppate prima dell'invio all'archivio dati. Le altre istruzioni in un batch, archiviare meno round trip per i dati.|
|Memorizzare nella cache le righe figlio (DBPROP_ADC_CACHECHILDROWS)|Per i recordset creato con il Data shaping, questo valore indica se Recordset figlio vengono archiviati in una cache per un uso successivo.|
|Versione del motore del cursore (DBPROP_ADC_CEVER)|Indica la versione del servizio di cursore in uso.|
|Gestire lo stato di modifica (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica il testo del comando utilizzato per la risincronizzazione un una o più righe in un join tra più tabelle.|
|[Ottimizzazione](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica se è necessario creare un indice. Se impostato su **True**, autorizza la creazione di indici per migliorare l'esecuzione di determinate operazioni temporanea.|
|[Proprietà dinamica Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica il nome del **Recordset**. Può essere riferimento corrente oppure la successiva, i comandi di shaping dei dati.|
|[La risincronizzazione di comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica una stringa di comando personalizzato utilizzato dal [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo quando la [tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) proprietà è attiva.|
|[Catalogo univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome del database contenente la tabella a cui fa riferimento il **Unique Table** proprietà.|
|[Schema univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome del proprietario della tabella a cui fa riferimento il **Unique Table** proprietà.|
|[Tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome di una tabella in un **Recordset** creati da più tabelle che possono essere modificate da inserimenti, aggiornamenti o eliminazioni.|
|Criteri di aggiornamento (DBPROP_ADC_UPDATECRITERIA)|Indica quali campi nel **in cui** clausola vengono usati per gestire i conflitti che si verificano durante un aggiornamento.|
|[Aggiornare la risincronizzazione](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica se il **Risincronizza** metodo viene richiamato in modo implicito dopo la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo (e il relativo comportamento), quando il **tabella univoca** proprietà è attiva.|

 È anche possibile impostare o recuperare una proprietà dinamica specificandone il nome dell'indice per la **proprietà** raccolta. Ad esempio, ottenere e visualizzare il valore corrente del [Ottimizza](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) proprietà dinamica, quindi impostare un nuovo valore, come indicato di seguito:

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamento delle proprietà predefinite
 Cursor Service per OLE DB influisce anche sul comportamento di determinate proprietà predefinite.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Integra i tipi di cursori che sono disponibili per un **Recordset**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Integra i tipi di blocchi disponibili per un **Recordset**. Abilita aggiornamenti in batch.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Specifica i nomi dei campi di uno o più che il **Recordset** viene ordinato se e in ogni campo viene ordinato in ordine crescente o decrescente.|

## <a name="method-behavior"></a>Comportamento del metodo
 Cursor Service per OLE DB consente di abilitare o influisce sul comportamento dei [campo](../../../ado/reference/ado-api/field-object.md) dell'oggetto [Append](../../../ado/reference/ado-api/append-method-ado.md) metodo; e il **Recordset** dell'oggetto [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [salvare](../../../ado/reference/ado-api/save-method.md) metodi.
