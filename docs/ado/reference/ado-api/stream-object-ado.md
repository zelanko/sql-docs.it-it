---
title: Oggetto Stream (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c70a22a3048c769aac343d51e621e4d755d3baeb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916727"
---
# <a name="stream-object-ado"></a>Oggetto Stream (ADO)
Rappresenta un flusso di dati binari o testo.  
  
 Nelle gerarchie strutturate ad albero quali un file system o un sistema di posta elettronica, è possibile che a un [record](../../../ado/reference/ado-api/record-object-ado.md) sia associato un flusso binario predefinito di bit che contenga il contenuto del file o del messaggio di posta elettronica. Un oggetto **flusso** può essere usato per modificare campi o record contenenti questi flussi di dati. È possibile ottenere un oggetto **flusso** nei modi seguenti:  
  
-   Da un URL che punta a un oggetto (in genere un file) contenente dati binari o di testo. Questo oggetto può essere un documento semplice, un oggetto **record** che rappresenta un documento strutturato o una cartella.  
  
-   Aprendo l'oggetto **flusso** predefinito associato a un oggetto **record** . È possibile ottenere il flusso predefinito associato a un oggetto **record** quando il **record** viene aperto, per eliminare un round trip solo per aprire il flusso.  
  
-   Creando un'istanza di un oggetto **flusso** . Questi oggetti **flusso** possono essere usati per archiviare i dati ai fini dell'applicazione. A differenza di un **flusso** associato a un URL o al **flusso** predefinito di un **record**, per impostazione predefinita un **flusso** di cui è stata creata un'istanza non ha alcuna associazione con un'origine sottostante.  
  
 Con i metodi e le proprietà di un oggetto **flusso** , è possibile eseguire le operazioni seguenti:  
  
-   Aprire un oggetto **flusso** da un **record** o un URL con il metodo [Open](../../../ado/reference/ado-api/open-method-ado-stream.md) .  
  
-   Chiudere un **flusso** con il metodo [Close](../../../ado/reference/ado-api/close-method-ado.md) .  
  
-   Byte di input o testo in un **flusso** con i metodi [Write](../../../ado/reference/ado-api/write-method.md) e [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md) .  
  
-   Leggere i byte dal **flusso** con i metodi [Read](../../../ado/reference/ado-api/read-method.md) e [READTEXT](../../../ado/reference/ado-api/readtext-method.md) .  
  
-   Scrivere i dati di **flusso** ancora presenti nel buffer ADO nell'oggetto sottostante con il metodo [Flush](../../../ado/reference/ado-api/flush-method-ado.md) .  
  
-   Copiare il contenuto di un **flusso** in un altro **flusso** con il metodo [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) .  
  
-   Controllare il modo in cui le righe vengono lette dal file di origine con il metodo [SkipLine](../../../ado/reference/ado-api/skipline-method.md)e la proprietà [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) .  
  
-   Determinare la fine della posizione del flusso con la proprietà [EOS](../../../ado/reference/ado-api/eos-property.md)e il metodo [SetEOS](../../../ado/reference/ado-api/seteos-method.md) .  
  
-   Salvare e ripristinare i dati nei file con i metodi [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)e [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) .  
  
-   Specificare il set di caratteri utilizzato per archiviare il **flusso** con la proprietà [CharSet](../../../ado/reference/ado-api/charset-property-ado.md) .  
  
-   Arrestare un'operazione di **flusso** asincrona con il metodo [Cancel](../../../ado/reference/ado-api/cancel-method-ado.md) .  
  
-   Determinare il numero di byte in un **flusso** con la proprietà [size](../../../ado/reference/ado-api/size-property-ado-stream.md) .  
  
-   Controllare la posizione corrente all'interno di un **flusso** con la proprietà [position](../../../ado/reference/ado-api/position-property-ado.md) .  
  
-   Determinare il tipo di dati in un **flusso** con la proprietà [Type](../../../ado/reference/ado-api/type-property-ado-stream.md) .  
  
-   Determinare lo stato corrente del **flusso** (chiuso, aperto o in esecuzione) con la proprietà [state](../../../ado/reference/ado-api/state-property-ado.md) .  
  
-   Specificare la modalità di accesso per il **flusso** con la proprietà [mode](../../../ado/reference/ado-api/mode-property-ado.md) .  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 L'oggetto **flusso** è sicuro per lo scripting.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Stream](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Record e flussi](../../../ado/guide/data/records-and-streams.md)
