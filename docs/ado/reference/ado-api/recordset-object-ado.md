---
title: Oggetto recordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e76bc993b6f3fed781b8458bc7cf4a70081cd167
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931368"
---
# <a name="recordset-object-ado"></a>Oggetto Recordset (ADO)
Rappresenta l'intero set di record di una tabella di base o i risultati di un comando eseguito. In qualsiasi momento, l'oggetto **Recordset** fa riferimento solo a un singolo record all'interno del set come record corrente.  
  
## <a name="remarks"></a>Osservazioni  
 Si utilizzano oggetti **Recordset** per modificare i dati da un provider. Quando si utilizza ADO, i dati vengono modificati quasi interamente utilizzando oggetti **Recordset** . Tutti gli oggetti **Recordset** sono costituiti da record (righe) e campi (colonne). A seconda della funzionalità supportata dal provider, alcuni metodi o proprietà del **Recordset** potrebbero non essere disponibili.  
  
 Oggetto ADODB. Recordset è il ProgID da utilizzare per creare un oggetto **Recordset** . Applicazioni esistenti che fanno riferimento all'oggetto adore obsoleto. Il ProgID del recordset continuerà a funzionare senza ricompilare, ma il nuovo sviluppo dovrebbe fare riferimento a ADODB. Recordset.  
  
 In ADO sono definiti quattro tipi di cursore diversi:  
  
-   **Cursore dinamico** Consente di visualizzare aggiunte, modifiche ed eliminazioni da parte di altri utenti. consente a tutti i tipi di spostamento tramite il **Recordset** che non si basa sui segnalibri. e consente ai segnalibri se supportati dal provider.  
  
-   **Cursore keyset** Si comporta come un cursore dinamico, ad eccezione del fatto che impedisce di visualizzare i record aggiunti da altri utenti e impedisce l'accesso ai record eliminati da altri utenti. Le modifiche ai dati da parte di altri utenti saranno ancora visibili. Supporta sempre segnalibri e pertanto consente tutti i tipi di spostamento tramite il **Recordset**.  
  
-   **Cursore statico** Fornisce una copia statica di un set di record da usare per trovare i dati o generare report; consente sempre i segnalibri e pertanto consente tutti i tipi di spostamento tramite il **Recordset**. Aggiunte, modifiche o eliminazioni da parte di altri utenti non saranno visibili. Si tratta dell'unico tipo di cursore consentito quando si apre un oggetto **Recordset** lato client.  
  
-   **Cursore di sola trasmissione** Consente di scorrere in modo semplice il **Recordset**. Aggiunte, modifiche o eliminazioni da parte di altri utenti non saranno visibili. Ciò consente di migliorare le prestazioni nelle situazioni in cui è necessario eseguire un singolo passaggio attraverso un **Recordset**.  
  
 Impostare la proprietà [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) prima di aprire il **Recordset** per scegliere il tipo di cursore oppure passare un argomento *CursorType* con il metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) . Alcuni provider non supportano tutti i tipi di cursore. Controllare la documentazione del provider. Se non si specifica un tipo di cursore, ADO apre per impostazione predefinita un cursore di tipo "inoltr".  
  
 Se la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient** per aprire un **Recordset**, la proprietà **UnderlyingValue** sugli oggetti [Field](../../../ado/reference/ado-api/field-object.md) non è disponibile nell'oggetto **Recordset** restituito. Se utilizzata con alcuni provider, ad esempio il provider ODBC Microsoft per OLE DB insieme a Microsoft SQL Server, è possibile creare oggetti **Recordset** indipendentemente da un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) definito in precedenza passando una stringa di connessione con il metodo **Open** . ADO crea ancora un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) , ma non assegna tale oggetto a una variabile oggetto. Tuttavia, se si aprono più oggetti **Recordset** sulla stessa connessione, è necessario creare e aprire un oggetto **connessione** in modo esplicito; in questo modo l'oggetto **connessione** viene assegnato a una variabile oggetto. Se non si utilizza questa variabile oggetto quando si aprono oggetti **Recordset** , ADO crea un nuovo oggetto **connessione** per ogni nuovo **Recordset**, anche se si passa la stessa stringa di connessione.  
  
 È possibile creare tutti gli oggetti **Recordset** necessari.  
  
 Quando si apre un **Recordset**, il record corrente viene posizionato sul primo record, se presente, e le proprietà [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) sono impostate su **false**. Se non sono presenti record, le impostazioni della proprietà **BOF** e **EOF** sono **true**.  
  
 È possibile usare i metodi [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**e **MovePrevious** ; metodo [Move](../../../ado/reference/ado-api/move-method-ado.md) ; e le proprietà [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)e [Filter](../../../ado/reference/ado-api/filter-property.md) per riposizionare il record corrente, presupponendo che il provider supporti la funzionalità pertinente. Gli oggetti **Recordset** di sola trasmissione supportano solo il metodo [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) . Quando si usano i metodi **Move** per visitare ogni record (o enumerare **il recordset**), è possibile usare le proprietà **BOF** e **EOF** per determinare se è stato spostato oltre l'inizio o la fine del **Recordset**.  
  
 Prima di utilizzare qualsiasi funzionalità di un oggetto **Recordset** , è necessario chiamare il metodo **Supports** sull'oggetto per verificare che la funzionalità sia supportata o disponibile. Non è necessario usare la funzionalità quando il metodo **Supports** restituisce false. Ad esempio, è possibile usare il metodo **MovePrevious** solo se `Recordset.Supports(adMovePrevious)` restituisce **true**. In caso contrario, verrà visualizzato un errore perché l'oggetto **Recordset** potrebbe essere stato chiuso e la funzionalità non è stata resa disponibile nell'istanza. Se una funzionalità a cui si è interessati non è supportata, **Supports** restituirà anche false. In questo caso, è consigliabile evitare di chiamare la proprietà o il metodo corrispondente nell'oggetto **Recordset** .  
  
 Gli oggetti **Recordset** possono supportare due tipi di aggiornamento: immediato e in batch. Nell'aggiornamento immediato, tutte le modifiche ai dati vengono scritte immediatamente nell'origine dati sottostante una volta chiamato il metodo [Update](../../../ado/reference/ado-api/update-method.md) . È anche possibile passare matrici di valori come parametri con i metodi [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) e **Update** e aggiornare contemporaneamente più campi in un record.  
  
 Se un provider supporta l'aggiornamento in batch, è possibile fare in modo che la cache del provider cambi a più di un record e quindi trasmetterli in una singola chiamata al database con il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . Questo vale per le modifiche apportate con i metodi **AddNew**, **Update**e [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) . Dopo aver chiamato il metodo **UpdateBatch** , è possibile usare la proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) per verificare la presenza di conflitti di dati per risolverli.  
  
> [!NOTE]
>  Per eseguire una query senza usare un oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) , passare una stringa di query al metodo **Open** di un oggetto **Recordset** . Tuttavia, è necessario un oggetto **comando** quando si desidera salvare in modo permanente il testo del comando ed eseguirlo di nuovo oppure utilizzare parametri di query.  
  
 La proprietà [mode](../../../ado/reference/ado-api/mode-property-ado.md) governa le autorizzazioni di accesso.  
  
 La raccolta **Fields** è il membro predefinito dell'oggetto **Recordset** . Di conseguenza, le due istruzioni di codice seguenti sono equivalenti.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Quando un oggetto **Recordset** viene passato tra i processi, viene eseguito il marshalling solo dei valori dei **set di righe** e le proprietà dell'oggetto **Recordset** vengono ignorate. Durante l'operazione di unmarshalling, il **set di righe** viene decompresso in un oggetto **Recordset** appena creato, che imposta anche le proprietà sui valori predefiniti.  
  
 L'oggetto **Recordset** è sicuro per lo scripting.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto recordset](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Appendice A: Provider](../../../ado/guide/appendixes/appendix-a-providers.md)
