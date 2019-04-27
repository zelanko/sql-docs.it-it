---
title: Registrare l'oggetto (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d719ebf47757a48b034d2a0cadd0ed68f51f0ee5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62661632"
---
# <a name="record-object-ado"></a>Oggetto Record (ADO)
Rappresenta una riga da una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o il provider di dati o un oggetto restituito da un provider di dati semistrutturati, ad esempio un file o directory.  
  
## <a name="remarks"></a>Note  
 Oggetto **Record** oggetto rappresenta una riga di dati e presenta alcune analogie con una sola riga concettuale **Recordset**. A seconda delle funzionalità del provider, **Record** oggetti possono essere restituiti direttamente dal provider invece di una riga singola **Recordset**, ad esempio quando una query SQL che seleziona solo una riga è eseguito. Oppure, un **Record** oggetto può essere ottenuto direttamente da un **Recordset** oggetto. Oppure, un **Record** può essere restituito direttamente da un provider di dati semistrutturati, ad esempio il provider OLE DB di Microsoft Exchange.  
  
 È possibile visualizzare i campi associati i **Record** dell'oggetto per mezzo del [campi](../../../ado/reference/ado-api/fields-collection-ado.md) insieme nel **Record** oggetto. ADO consente le colonne con valori di oggetto inclusi **Recordset**, **SafeArray**e i valori scalari il **campi** raccolta di **Record** oggetti.  
  
 Se il **Record** oggetto rappresenta una riga in un **Recordset**, è possibile tornare a questo originale **Recordset** con il [origine](../../../ado/reference/ado-api/source-property-ado-record.md) proprietà.  
  
 Il **Record** oggetto può anche essere utilizzato dai provider di dati semistrutturati, ad esempio le [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), alla struttura ad albero degli spazi dei nomi del modello. Ogni nodo nell'albero è un **Record** oggetto con le colonne associate. Le colonne possono rappresentare gli attributi di tale nodo e altre informazioni rilevanti. Il **Record** oggetto può rappresentare sia un nodo foglia e un nodo foglia della struttura ad albero. I nodi non foglia sono gli altri nodi come i relativi contenuti, ma i nodi foglia sono privi di tale contenuto. I nodi foglia contengono in genere i flussi binari di dati e i nodi non foglia possono anche essere un flusso binario predefinito associato. Proprietà di **Record** oggetto che identifica il tipo di nodo.  
  
 Il **Record** oggetto rappresenta inoltre un modo alternativo per lo spostamento in una struttura gerarchica organizzati i dati. Oggetto **Record** oggetto può essere creata per rappresentare la radice di un sottoalbero specifico in una struttura ad albero di grandi dimensioni e nuovi **Record** gli oggetti possono essere aperti per rappresentare i nodi figlio.  
  
 Una risorsa (ad esempio, un file o directory) può essere identificata in modo univoco tramite un URL assoluto. Oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto in modo implicito viene creato e impostato il **Record** oggetto quando il **Record** viene aperto usando un URL assoluto. Oggetto **connessione** oggetto può essere impostato in modo esplicito il **Record** dell'oggetto tramite il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà. I file e directory in cui è possibile accedere usando il **connessione** oggetto definiscono il *contesto* in cui **Record** possono verificarsi operazioni.  
  
 Metodi di modifica e l'esplorazione dei dati sul **Record** oggetto accettano anche un URL relativo, che consente di individuare una risorsa tramite un URL assoluto o la **connessione** contesto dell'oggetto come un punto di partenza.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Oggetto **Connection** oggetto è associato a ogni **Record** oggetto. Pertanto **Record** operazioni di oggetto possono essere parte di una transazione richiamando **connessione** oggetto metodi di transazione.  
  
 Il **Record** oggetto non supporta gli eventi ADO e pertanto non risponderà alle notifiche.  
  
 Con i metodi e proprietà di un **Record** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Impostare o restituire l'oggetto associato **Connection** dell'oggetto con il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà.  
  
-   Indicare le autorizzazioni di accesso con il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà.  
  
-   Restituisce l'URL della directory, se presente, che contiene la risorsa rappresentata dal **Record** con il [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) proprietà.  
  
-   Indicare l'URL assoluto, relativo URL, oppure **Recordset** da cui il **Record** deriva con il [origine](../../../ado/reference/ado-api/source-property-ado-record.md) proprietà.  
  
-   Indicare lo stato corrente del **Record** con il [stato](../../../ado/reference/ado-api/state-property-ado.md) proprietà.  
  
-   Indicare il tipo di **Record** - *semplice*, *raccolta*, o *documenti strutturati* : con la [ RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)proprietà.  
  
-   Arrestare l'esecuzione di un'operazione asincrona con il [annullare](../../../ado/reference/ado-api/cancel-method-ado.md) (metodo).  
  
-   Dissociare il **Record** da un'origine dati con il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) (metodo).  
  
-   Copiare il file o directory rappresentata da un **Record** in un'altra posizione con il [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) (metodo).  
  
-   Eliminare il file o directory e sottodirectory, rappresentato da un **Record** con il [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) (metodo).  
  
-   Aprire una **Recordset** che contiene le righe che rappresentano le sottodirectory e i file dell'entità rappresentata dalle **Record** con il [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) (metodo).  
  
-   Spostare o rinominare il file o directory e sottodirectory, rappresentato da un **Record** in un'altra posizione con il [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) (metodo).  
  
-   Associare il **Record** con i dati esistenti di origine oppure creare un nuovo file o directory con la [Open](../../../ado/reference/ado-api/open-method-ado-record.md) (metodo).  
  
 Il **Record** oggetto è sicuro per lo scripting.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Record](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Fields Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [I record e i flussi](../../../ado/guide/data/records-and-streams.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
