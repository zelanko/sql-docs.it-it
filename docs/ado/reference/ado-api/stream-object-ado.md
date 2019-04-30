---
title: Stream oggetto (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 976e822482efc530e3b055f61c242ee03a30e012
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63179837"
---
# <a name="stream-object-ado"></a>Oggetto Stream (ADO)
Rappresenta un flusso di dati binari o testo.  
  
 Nelle gerarchie di struttura ad albero, ad esempio un file system o un sistema di posta elettronica, un [Record](../../../ado/reference/ado-api/record-object-ado.md) può essere un flusso di binari predefinito di bit associato che include il contenuto del file o posta elettronica. Oggetto **Stream** oggetto può essere utilizzato per modificare i campi o record che contengono questi flussi di dati. Oggetto **Stream** oggetto può essere ottenuto nei modi seguenti:  
  
-   Da un URL che punta a un oggetto (in genere un file) contenente dati binari o testo. Questo oggetto può essere un semplice documento, un **Record** oggetto che rappresenta un documento strutturato o in una cartella.  
  
-   Aprendo il valore predefinito **Stream** oggetto associato a un **Record** oggetto. È possibile ottenere il flusso predefinito associato con un **Record** oggetto quando il **Record** viene aperto, per eliminare un round trip per aprire il flusso.  
  
-   Creando un **Stream** oggetto. Questi **Stream** oggetti possono essere utilizzati per archiviare i dati ai fini dell'applicazione. A differenza di una **Stream** associato a un URL o il valore predefinito **Stream** di un **Record**, un'istanza **Stream** non ha alcuna associazione con un origine sottostante per impostazione predefinita.  
  
 Con i metodi e proprietà di un **Stream** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Aprire un **Stream** dell'oggetto da un **Record** o l'URL con il [Open](../../../ado/reference/ado-api/open-method-ado-stream.md) (metodo).  
  
-   Chiudi una **Stream** con il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) (metodo).  
  
-   Input byte o il testo da un **Stream** con il [scrivere](../../../ado/reference/ado-api/write-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md) metodi.  
  
-   Leggere i byte dal **Stream** con il [lettura](../../../ado/reference/ado-api/read-method.md) e [ReadText](../../../ado/reference/ado-api/readtext-method.md) metodi.  
  
-   Scrivere eventuali **Stream** dati ancora in ADO buffer all'oggetto sottostante con il [Flush](../../../ado/reference/ado-api/flush-method-ado.md) (metodo).  
  
-   Copiare il contenuto di un **Stream** a un'altra **Stream** con il [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) (metodo).  
  
-   Controllare come le righe vengono lette dal file di origine con il [SkipLine](../../../ado/reference/ado-api/skipline-method.md)metodo e il [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) proprietà.  
  
-   Determinare la fine della posizione di flusso con il [EOS](../../../ado/reference/ado-api/eos-property.md)proprietà e [SetEOS](../../../ado/reference/ado-api/seteos-method.md) (metodo).  
  
-   Salvare e ripristinare i dati in file con il [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)e [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) metodi.  
  
-   Specificare il set di caratteri utilizzato per archiviare il **Stream** con il [Charset](../../../ado/reference/ado-api/charset-property-ado.md) proprietà.  
  
-   HALT asincrono **Stream** operazione con il [Annulla](../../../ado/reference/ado-api/cancel-method-ado.md) (metodo).  
  
-   Determinare il numero di byte in una **Stream** con il [dimensioni](../../../ado/reference/ado-api/size-property-ado-stream.md) proprietà.  
  
-   Controllare la posizione corrente all'interno di un **Stream** con il [posizione](../../../ado/reference/ado-api/position-property-ado.md) proprietà.  
  
-   Determinare il tipo di dati in un **Stream** con il [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) proprietà.  
  
-   Determinare lo stato corrente del **Stream** (chiuso, aperto, o l'esecuzione) con i [stato](../../../ado/reference/ado-api/state-property-ado.md) proprietà.  
  
-   Specificare la modalità di accesso per il **Stream** con il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Il **Stream** oggetto è sicuro per lo scripting.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Le proprietà dell'oggetto Stream, metodi ed eventi](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Record e flussi](../../../ado/guide/data/records-and-streams.md)
