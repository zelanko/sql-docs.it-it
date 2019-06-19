---
title: Metodo (Recordset ADO) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9aee9b4f6054b5cbfca41db35f34a27000a7ac01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719214"
---
# <a name="open-method-ado-recordset"></a>Metodo Open (Recordset - ADO)
Apre un cursore in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **Variant** che restituisce un valore valido [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto, un'istruzione SQL, un nome di tabella, una chiamata alla stored procedure, un URL o il nome di un file oppure [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto contenente un archiviati in modo permanente [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 *ActiveConnection*  
 Facoltativo. Entrambi una **Variant** che restituisce un valore valido [connessione](../../../ado/reference/ado-api/connection-object-ado.md) nome della variabile oggetto, o un **stringa** contenente [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) parametri.  
  
 *CursorType*  
 Facoltativo. Oggetto [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valore che determina il tipo di cursore che il provider deve utilizzare quando si apre il **Recordset**. Il valore predefinito è **adOpenForwardOnly**.  
  
 *LockType*  
 Facoltativo. Oggetto [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valore che determina il tipo di blocco (concorrenza) il provider deve utilizzare quando si apre il **Recordset**. Il valore predefinito è **adLockReadOnly**.  
  
 *Opzioni*  
 Facoltativo. Oggetto **lungo** valore che indica come il provider deve valutare il *origine* argomento se rappresenta un elemento diverso da un **comando** oggetto o che il **Recordset** deve essere ripristinato da un file in cui è stato precedentemente salvato. Può essere uno o più [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) oppure [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valori, che possono essere combinati con un operatore OR bit per bit.  
  
> [!NOTE]
>  Se si apre un **Recordset** da un **Stream** contenenti un persistente **Recordset**, usando un [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valore **adAsyncFetchNonBlocking** non avrà effetto; l'operazione di recupero sarà sincrona e bloccante.  
  
> [!NOTE]
>  Il **ExecuteOpenEnum** i valori di **adExecuteStream** oppure **adExecuteStream** non devono essere usati con **Open**.  
  
## <a name="remarks"></a>Note  
 Il cursore predefinito per un oggetto ADO **Recordset** è un cursore forward-only di sola lettura che si trova nel server.  
  
 Usando il **aperto** metodo su un **Recordset** oggetto viene aperto un cursore che rappresenta i record da una tabella di base, i risultati di una query o salvato in precedenza **Recordset**.  
  
 Usare l'opzione facoltativa *origine* argomento per specificare un'origine dati usando uno dei seguenti: un **comando** variabile oggetto, un'istruzione SQL, una stored procedure, un nome di tabella, un URL o un nome di percorso completo del file. Se *origine* è un nome di percorso di file, può essere un percorso completo ("c:\dir\file.rst"), un percorso relativo (".. \File.rst"), o un URL ("<https://files/file.rst>").  
  
 Non è consigliabile usare la *origine* argomento delle **Open** metodo per eseguire una query di comando che non restituisce i record in quanto non esiste un modo semplice per determinare se la chiamata ha avuto esito positivo. Il **Recordset** restituito da ad una query verrà chiusa. Per eseguire una query che restituiscono record, ad esempio un'istruzione SQL INSERT, chiamare il [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) metodo di un **comando** oggetto o nella [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) metodo di un [Connessione](../../../ado/reference/ado-api/connection-object-ado.md) invece dell'oggetto.  
  
 Il *ActiveConnection* argomento corrisponde alla [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà e specifica la connessione in cui per aprire il **Recordset** oggetto. Se si passa una definizione della connessione per questo argomento, ADO apre una nuova connessione utilizzando i parametri specificati. Dopo aver aperto la **Recordset** con un cursore lato client impostando il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**, è possibile modificare il valore di questa proprietà per l'invio aggiornamenti a un altro provider. Oppure è possibile impostare questa proprietà su **Nothing** (in Microsoft Visual Basic) oppure NULL per disconnettere il **Recordset** da qualsiasi provider. Modificando *ActiveConnection* per un cursore lato server genera un errore, tuttavia.  
  
 Per gli altri argomenti che corrispondono direttamente alle proprietà di un **Recordset** oggetto (*origine*, *CursorType*, e *LockType*), la relazione degli argomenti per la proprietà è come segue:  
  
-   La proprietà è di lettura/scrittura prima la **Recordset** apertura dell'oggetto.  
  
-   Le impostazioni delle proprietà vengono utilizzate solo se si passano gli argomenti corrispondenti quando si esegue la **aperto** (metodo). Se si passa un argomento, viene eseguito l'override dell'impostazione di proprietà corrispondente e l'impostazione della proprietà viene aggiornata con il valore dell'argomento.  
  
-   Dopo aver aperto la **Recordset** dell'oggetto, tali proprietà diventeranno di sola lettura.  
  
> [!NOTE]
>  Il **ActiveConnection** proprietà è di sola lettura per **Recordset** oggetti la cui proprietà [origine](../../../ado/reference/ado-api/source-property-ado-recordset.md) è impostata su un valore valido **comando** oggetto, anche se il **Recordset** oggetto non è aperto.  
  
 Se si passa un' **comando** dell'oggetto nel *origine* argomento e inoltre passare un' *ActiveConnection* si verifica un errore di argomento,. Il **ActiveConnection** proprietà delle **comando** oggetto deve essere già impostato su un valore valido **connessione** oggetto o stringa di connessione.  
  
 Se si passa un valore diverso da un **comandi** dell'oggetto nel *origine* argomento, è possibile usare il *opzioni* argomento per ottimizzare la valutazione del *origine*  argomento. Se il *opzioni* argomento non è definito, potrebbero verificarsi effetti negativi sulle prestazioni poiché ADO debba effettuare chiamate al provider per determinare se l'argomento è un'istruzione SQL, una stored procedure, un URL o un nome di tabella. Se si sa cosa *origine* tipo in uso, impostando il *opzioni* argomento indica ad ADO per passarvi direttamente il codice pertinente. Se il *le opzioni* argomento non corrisponde la *origine* digitare, si verifica un errore.  
  
 Se si passa un' **Stream** dell'oggetto nel *origine* argomento, si evita di passare le informazioni negli altri argomenti. In questo modo verrà generato un errore. Il **ActiveConnection** informazioni non sono mantenute quando una **Recordset** viene aperto da un **Stream**.  
  
 Il valore predefinito per il *le opzioni* l'argomento è **adCmdFile** se nessuna connessione è associata la **Recordset**. Si tratterà in genere il caso per memorizzare in modo persistente **Recordset** oggetti.  
  
 Se l'origine dati non restituisce Nessun record, il provider imposta sia i [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) le proprietà da **True**, e la posizione corrente non è definita. È comunque possibile aggiungere nuovi dati vuoto a questo **Recordset** se il tipo di cursore consente dell'oggetto.  
  
 Quando aver concluso le operazioni su un oggetto aperto **Recordset** dell'oggetto, utilizzare il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodo da liberare eventuali risorse di sistema associate. Chiusura di un oggetto senza rimuoverlo dalla memoria. è possibile modificare le impostazioni delle proprietà e usare la **aprire** metodo aprirlo più tardi. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto *Nothing*.  
  
 Prima la **ActiveConnection** è impostata, chiamare **Open** senza operandi per creare un'istanza di un **Recordset** creati mediante l'aggiunta di campi dal  **Recordset** [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta.  
  
 Se è stato impostato il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**, è possibile recuperare le righe in modo asincrono in uno dei due modi. Il metodo consigliato consiste nell'impostare *le opzioni* al **adAsyncFetch**. In alternativa, è possibile usare la proprietà dinamica "Asynchronous Processing set di righe" nella [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta, ma gli eventi recuperati correlati possono andare persi se non si imposta la *opzioni* parametro **adAsyncFetch**.  
  
> [!NOTE]
>  Il recupero in background nel provider di MS Remote è supportato solo tramite il **aperto** del metodo *opzioni* parametro.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Alcune combinazioni di [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valori non sono validi. Per informazioni su quali non è possibile combinare le opzioni, vedere gli argomenti per il [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Esempio di metodi Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Esempio di metodi Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Salvare e aprire l'esempio di metodi (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Esempio di metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
