---
description: Servizio Microsoft Cursor per OLE DB (componente servizio ADO)
title: Servizio Microsoft Cursor per OLE DB (componente servizio ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f83f151331fe483400edda90d7deb7c469b5574
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444553"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Panoramica di Microsoft Cursor Service per OLE DB
Il servizio Microsoft Cursor per OLE DB integra le funzioni di supporto del cursore dei provider di dati. Di conseguenza, l'utente percepisce una funzionalità relativamente uniforme di tutti i provider di dati.

 Il servizio Cursor rende disponibili le proprietà dinamiche e migliora il comportamento di alcuni metodi. Ad esempio, la proprietà [ottimizza](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dinamica consente la creazione di indici temporanei per facilitare determinate operazioni, ad esempio il metodo [Find](../../../ado/reference/ado-api/find-method-ado.md) .

 Il servizio Cursor Abilita il supporto per l'aggiornamento in batch in tutti i casi. Simula inoltre tipi di cursore più idonei, ad esempio cursori dinamici, quando un provider di dati può fornire solo cursori meno idonei, ad esempio i cursori statici.

## <a name="keyword"></a>Parola chiave
 Per richiamare questo componente del servizio, impostare la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) dell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o della [connessione](../../../ado/reference/ado-api/connection-object-ado.md) su **adUseClient**.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Quando viene richiamato il servizio Cursor per OLE DB, le proprietà dinamiche seguenti vengono aggiunte alla raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto **Recordset** . L'elenco completo delle proprietà dinamiche degli oggetti di **connessione** e **Recordset** è elencato nell' [indice della proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). I nomi delle proprietà OLE DB associate, laddove appropriato, sono inclusi tra parentesi dopo il nome della proprietà ADO.

 Le modifiche apportate ad alcune proprietà dinamiche non sono visibili all'origine dati sottostante dopo che è stato richiamato il servizio Cursor. Se ad esempio si imposta la proprietà *timeout comando* in un **Recordset** , il provider di dati sottostante non sarà visibile.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Se l'applicazione richiede il servizio Cursor, ma è necessario impostare le proprietà dinamiche sul provider sottostante, impostare le proprietà prima di richiamare il servizio Cursor. Le impostazioni delle proprietà dell'oggetto comando vengono sempre passate al provider di dati sottostante indipendentemente dalla posizione del cursore. È pertanto possibile utilizzare un oggetto Command anche per impostare le proprietà in qualsiasi momento.

> [!NOTE]
>  La proprietà dinamica DBPROP_SERVERDATAONINSERT non è supportata dal servizio cursore, anche se è supportata dal provider di dati sottostante.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|Ricalcolo automatico (DBPROP_ADC_AUTORECALC)|Per i recordset creati con il servizio Data Shaping, questo valore indica la frequenza con cui vengono calcolate le colonne calcolate e di aggregazione. Il valore predefinito (valore = 1) prevede il ricalcolo ogni volta che il servizio Data Shaping determina che i valori sono stati modificati. Se il valore è 0, le colonne calcolate o aggregate vengono calcolate solo quando la gerarchia viene inizialmente compilata.|
|Dimensioni batch (DBPROP_ADC_BATCHSIZE)|Indica il numero di istruzioni Update che possono essere raggruppate prima di essere inviate all'archivio dati. Più istruzioni in un batch, minore è il numero di round trip all'archivio dati.|
|Memorizzare nella cache le righe figlio (DBPROP_ADC_CACHECHILDROWS)|Per i recordset creati con il servizio Data Shaping, questo valore indica se i recordset figlio vengono archiviati in una cache per un uso successivo.|
|Versione del motore di cursore (DBPROP_ADC_CEVER)|Indica la versione del servizio cursore utilizzata.|
|Mantieni stato delle modifiche (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica il testo del comando utilizzato per la risincronizzazione di una o più righe in un join a più tabelle.|
|[Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) (Ottimizza)|Indica se deve essere creato un indice. Se impostato su **true**, autorizza la creazione temporanea degli indici per migliorare l'esecuzione di determinate operazioni.|
|[Nome riforma](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica il nome del **Recordset**. È possibile fare riferimento all'interno dei comandi di data shaping correnti o successivi.|
|[Comando di risincronizzazione](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica una stringa di comando personalizzata utilizzata dal metodo [Resync](../../../ado/reference/ado-api/resync-method.md) quando è attiva la proprietà di [tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) .|
|[Catalogo univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome del database contenente la tabella a cui si fa riferimento nella proprietà di **tabella univoca** .|
|[Schema univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome del proprietario della tabella a cui si fa riferimento nella proprietà di **tabella univoca** .|
|[tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica il nome di una tabella in un **Recordset** creato da più tabelle che possono essere modificate da inserimenti, aggiornamenti o eliminazioni.|
|Criteri di aggiornamento (DBPROP_ADC_UPDATECRITERIA)|Indica i campi nella clausola **where** utilizzati per gestire i conflitti che si verificano durante un aggiornamento.|
|[Aggiornamento della risincronizzazione](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica se il metodo di **Risincronizzazione** viene richiamato in modo implicito dopo il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (e il relativo comportamento), quando è attiva la proprietà di **tabella univoca** .|

 È anche possibile impostare o recuperare una proprietà dinamica specificandone il nome come indice della raccolta **Properties** . Ottenere, ad esempio, il valore corrente della proprietà [optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) Dynamic, quindi impostare un nuovo valore, come indicato di seguito:

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamento della proprietà incorporata
 Il servizio Cursor per OLE DB influisca anche sul comportamento di determinate proprietà predefinite.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Integra i tipi di cursori disponibili per un **Recordset**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Integra i tipi di blocchi disponibili per un **Recordset**. Abilita gli aggiornamenti batch.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Specifica uno o più nomi di campo in base ai quali viene ordinato il **Recordset** e indica se ogni campo viene ordinato in ordine crescente o decrescente.|

## <a name="method-behavior"></a>Comportamento del metodo
 Il servizio Cursor per OLE DB Abilita o influisca sul comportamento del metodo [Append](../../../ado/reference/ado-api/append-method-ado.md) dell'oggetto [campo](../../../ado/reference/ado-api/field-object.md) ; e i metodi [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)e [Save](../../../ado/reference/ado-api/save-method.md) dell'oggetto **Recordset** .
