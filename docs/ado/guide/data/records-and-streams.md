---
title: I record e i flussi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 19fc6e61a10e1a92f0f674a23d00f1e1b06a596c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701694"
---
# <a name="records-and-streams"></a>Record e flussi
ADO offre attualmente le [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto come il mezzo principale per l'accesso alle informazioni nelle origini dati, ad esempio database relazionali. Tuttavia, alcuni provider supportano il [Record](../../../ado/reference/ado-api/record-object-ado.md) e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetti come alternativa o complementari oggetti con cui è possono modificare i dati dai provider. Per informazioni specifiche sulla **Record** comportamento, vedere la documentazione del provider.  
  
## <a name="records"></a>Record  
 **Record** gli oggetti funzionano essenzialmente come riga singola **Recordset**s. Tuttavia **record** hanno funzionalità limitate rispetto ai **recordset** e dispongono di proprietà e metodi diversi. L'origine per i dati in un **Record** oggetto può essere un comando che restituisce una riga di dati dal provider. Usando **Record** oggetti anziché **Recordset** agli oggetti di ricevere i risultati da una query che restituisce una riga di dati Elimina il sovraccarico di un'istanza più è complessa **Recordset**  oggetto.  
  
 **Record** oggetti possono essere usato un altro scopo, in particolare con i provider per origini dati diverse dalle tradizionali database relazionali, ad esempio il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Molte delle informazioni che devono essere elaborate esiste, non come tabelle nel database, ma come messaggi in sistemi di posta elettronica e i file nei file modern System. Il **Record** e **Stream** oggetti facilitano l'accesso alle informazioni archiviate nelle origini diverso da database relazionali.  
  
 Il **Record** oggetto può rappresentare e gestire i dati, ad esempio file e directory in un file system o le cartelle e i messaggi in un sistema di posta elettronica. A tale scopo, l'origine per il **Record** può essere la riga corrente di un elemento aperto **Recordset**, un URL assoluto o un URL relativo in combinazione con un elemento aperto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
 In genere, un **Recordset** può essere utilizzato per rappresentare un contenitore o in una gerarchia, ad esempio una cartella o la directory padre. Oggetto **Record** può essere utilizzato per restituire informazioni specifiche su un nodo nel contenitore padre, ad esempio un file o un documento. Il motivo principale **record** vengono usati per rappresentare questo tipo di informazioni è che queste origini dei dati eterogenee. Ciò significa che ogni **Record** può avere un set diverso e un numero di campi. Tradizionali **recordset** contenente le righe da un database sono omogenee, il che significa che ogni riga ha lo stesso numero e tipo dei campi.  
  
 Per altre informazioni sull'uso di **Record** oggetti per l'elaborazione di questi dati eterogenei dai provider come Provider di pubblicazione, vedere [utilizzo di ADO per Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Flussi  
 Il **Stream** oggetto fornisce i mezzi per leggere, scrivere e gestire un flusso di byte. Questo flusso di byte può essere testo o binari e dimensioni è limitato solo dalle risorse di sistema. In genere, ADO **Stream** gli oggetti vengono usati per gli scopi seguenti:  
  
-   Per contenere i dati di un **Recordset** salvati in formato XML. Questi flussi XML da salvare **Recordset**s è utilizzabile come origine quando si apre un nuovo **Recordset**. Per altre informazioni, vedere [flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Per contenere [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) da eseguire confrontandolo con il provider come alternativa alla [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Ad esempio, gli Updategram XML è utilizzabile come origine per un comando sul provider Microsoft OLE DB per SQL Server.  
  
-   Per ricevere i risultati dal provider in un formato diverso da un **Recordset**, ad esempio risultati XML di Provider Microsoft OLE DB per SQL Server. Per altre informazioni, vedere [recupero di set di risultati in flussi](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Per includere il testo o byte che costituiscono un file o un messaggio, in genere usati con i provider, ad esempio il Provider Microsoft OLE DB per Internet Publishing. Per altre informazioni su questo utilizzo di **Stream** oggetti, vedere [utilizzo di ADO per Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Oggetto **Stream** oggetto può essere aperto su:  
  
-   Un semplice file specificato con un URL.  
  
-   Un campo di un **Record** oppure **Recordset** contenenti un **Stream** oggetto.  
  
-   Il flusso predefinito di un **Record** oppure **Recordset** oggetto che rappresenta una directory o un file composto.  
  
-   Un campo di risorse contenente l'URL di file semplice.  
  
-   Nessuna origine particolare affatto. In questo caso, un **Stream** apertura dell'oggetto in memoria. I dati possono essere scritti in essa e quindi salvati in un altro **Stream** o file.  
  
-   Un campo BLOB in un **Recordset**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Flussi e persistenza](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Flussi di comandi](../../../ado/guide/data/command-streams.md)  
  
-   [Recupero di set di risultati nei flussi](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Uso di ADO per Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)
