---
title: Oggetto Recordset (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: cc95d6ef7e61dcde373a646359d134dce0b3389d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711939"
---
# <a name="recordset-object-ado"></a>Oggetto Recordset (ADO)
Rappresenta l'intero set di record da una tabella di base o i risultati di un comando eseguito. In qualsiasi momento, il **Recordset** oggetto fa riferimento a un singolo record all'interno del set come record corrente.  
  
## <a name="remarks"></a>Note  
 Si utilizza **Recordset** oggetti per modificare i dati da un provider. Quando si utilizza ADO, la modifica dei dati con quasi interamente **Recordset** oggetti. Tutti i **Recordset** gli oggetti sono costituiti da record (righe) e campi (colonne). A seconda della funzionalità supportata dal provider, alcuni **Recordset** metodi o proprietà potrebbe non essere disponibili.  
  
 OGGETTO ADODB. Recordset è il ProgID che dovrà essere usato per creare un **Recordset** oggetto. Applicazioni esistenti che fanno riferimento a ADOR obsoleti. Recordset ProgID continueranno a funzionare senza ricompilare, ma nuove attività di sviluppo deve fare riferimento a oggetto ADODB. Set di record.  
  
 Esistono quattro diversi tipi di cursore definiti in ADO:  
  
-   **Cursore dinamico** consente di visualizzare le aggiunte, modifiche ed eliminazioni da altri utenti; consente a tutti i tipi di spostamento all'interno di **Recordset** che non si basa su segnalibri; e consente i segnalibri, se il provider supporta essi.  
  
-   **Cursore keyset** aggiungere Behaves, ad esempio un cursore dinamico, ad eccezione del fatto che impedisce la visualizzazione record dagli altri utenti e impedisce l'accesso ai record eliminati dagli altri utenti. Le modifiche ai dati da altri utenti saranno ancora visibili. Sempre supporta i segnalibri e pertanto consente tutti i tipi di spostamento all'interno di **Recordset**.  
  
-   **Cursore statico** fornisce una copia statica di un set di record da usare per trovare i dati o per generare report; consente sempre i segnalibri e pertanto tutti i tipi di spostamento all'interno di **Recordset**. Le aggiunte, modifiche o eliminazioni da altri utenti non saranno visibili. Questo è l'unico tipo di cursore è consentito quando si apre un client-side **Recordset** oggetto.  
  
-   **Cursore forward-only** consente solo uno scorrimento in avanti tramite i **Recordset**. Le aggiunte, modifiche o eliminazioni da altri utenti non saranno visibili. Ciò migliora le prestazioni in situazioni in cui è necessario apportare solo una singola iterazione una **Recordset**.  
  
 Impostare il [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) proprietà prima dell'apertura il **Recordset** scegliere il tipo di cursore o passare una *CursorType* argomento con il [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)metodo. Alcuni provider non supporta tutti i tipi di cursore. Consultare la documentazione per il provider. Se non si specifica un tipo di cursore, ADO viene aperto un cursore forward-only per impostazione predefinita.  
  
 Se il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient** per aprire una **Recordset**, il **UnderlyingValue** proprietà [Campo](../../../ado/reference/ado-api/field-object.md) gli oggetti non è disponibile nell'oggetto restituito **Recordset** oggetto. Quando usato con alcuni provider (ad esempio il Provider ODBC di Microsoft per OLE DB in combinazione con Microsoft SQL Server), è possibile creare **Recordset** oggetti indipendentemente da un oggetto definito in precedenza [connessione](../../../ado/reference/ado-api/connection-object-ado.md)passando una stringa di connessione con il **Open** (metodo). ADO crea ancora un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto, ma tale oggetto non assegnato a una variabile oggetto. Tuttavia, se si sta aprendo più **Recordset** oggetti sulla stessa connessione, in modo esplicito è necessario creare e aprire un **connessione** oggetto; questo viene assegnato il **connessione**oggetto a una variabile oggetto. Se non si esegue questa variabile di oggetto quando si apre la **Recordset** oggetti, crea un nuovo oggetto ADO **connessione** oggetto per ogni nuovo **Recordset**, anche se si passa lo stesso stringa di connessione.  
  
 È possibile creare tanti **Recordset** gli oggetti in base alle esigenze.  
  
 Quando si apre un **Recordset**, il record corrente è posizionato sul primo record (se presente) e il [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) sono impostate su **False**. Se non sono presenti record, il **BOF** e **EOF** sono le impostazioni delle proprietà **True**.  
  
 È possibile usare la [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, e **MovePrevious** metodi; il [spostare](../../../ado/reference/ado-api/move-method-ado.md) metodo; e il [esempio di AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), e [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà da riposizionare il record corrente, presupponendo che il provider supporta pertinente funzionalità. Forward-only **Recordset** oggetti supportano solo le [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) (metodo). Quando si usa la **spostare** metodi per visitare ogni record (o enumerare le **Recordset**), è possibile usare il **BOF** e **EOF** proprietà da determinare se si è andati oltre l'inizio o alla fine del **Recordset**.  
  
 Prima di utilizzare qualsiasi funzionalità di un **Recordset** dell'oggetto, è necessario chiamare il **supporta** metodo sull'oggetto per verificare che la funzionalità è supportata o disponibile. Non è necessario usare la funzionalità quando la **supporta** metodo restituisce false. Ad esempio, è possibile usare la **MovePrevious** metodo solo se `Recordset.Supports(adMovePrevious)` restituisce **True**. In caso contrario, si verificherà un errore, perché il **Recordset** oggetto potrebbe essere stato chiuso e la funzionalità di rendering non disponibile nell'istanza. Se non è supportata una funzionalità che si è interessati, **supporta** restituirà false anche. In questo caso, è consigliabile evitare la chiamata la corrispondente proprietà o un metodo sul **Recordset** oggetto.  
  
 **Recordset** oggetti supporta due tipi di aggiornamento: immediata e in batch. Aggiornamento immediato, tutte le modifiche apportate ai dati vengono scritti immediatamente all'origine dati sottostante quando si chiama il [Update](../../../ado/reference/ado-api/update-method.md) (metodo). È anche possibile passare le matrici di valori come parametri con il [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) e **aggiornare** metodi e aggiornare contemporaneamente più campi in un record.  
  
 Se un provider supporta l'aggiornamento in batch, è possibile avere il provider di memorizzazione nella cache le modifiche a più di un record e quindi verranno trasmesse in una singola chiamata al database con il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (metodo). Questo vale per le modifiche apportate con il **AddNew**, **Update**, e [Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md) metodi. Dopo aver chiamato il **UpdateBatch** metodo, è possibile usare il [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà da controllare eventuali conflitti di dati per risolverli.  
  
> [!NOTE]
>  Per eseguire una query senza usare una [comando](../../../ado/reference/ado-api/command-object-ado.md) dell'oggetto, passare una stringa di query per il **Open** metodo di un **Recordset** oggetto. Tuttavia, un **comando** oggetto è obbligatorio quando si desidera salvare in modo permanente il testo del comando ed eseguirla di nuovo, oppure utilizzare i parametri di query.  
  
 Il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà determina le autorizzazioni di accesso.  
  
 Il **i campi** raccolta è il membro predefinito delle **Recordset** oggetto. Di conseguenza, le due istruzioni di codice seguenti sono equivalenti.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Quando un **Recordset** oggetto viene passato tra i processi, solo le **set di righe** valori vengono eseguito il marshalling e le proprietà del **Recordset** oggetto vengono ignorati. Durante l'unmarshalling, il **rowset** viene decompresso in una nuova istanza creata **Recordset** oggetto, che imposta anche le relative proprietà sui valori predefiniti.  
  
 Il **Recordset** oggetto è sicuro per lo scripting.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Le proprietà dell'oggetto Recordset, metodi ed eventi](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Appendice A: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
