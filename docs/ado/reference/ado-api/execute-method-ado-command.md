---
title: Eseguire il metodo (comando ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9508b85bc73ebbec82ad7d3bea5af5148d7c674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184803"
---
# <a name="execute-method-ado-command"></a>Metodo Execute (Command - ADO)
Esegue la query, l'istruzione SQL o stored procedure specificata nel [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) oppure [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) proprietà del [oggetto comando](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) riferimento all'oggetto, un flusso, o **Nothing**.  
  
#### <a name="parameters"></a>Parametri  
 *RecordsAffected*  
 Facoltativo. Oggetto **lungo** variabile in cui il provider restituisce il numero di record interessati dall'operazione. Il *RecordsAffected* parametro si applica solo per le query di comando o stored procedure. *RecordsAffected* non restituisce il numero di record restituiti da una query che restituiscono un risultato o una stored procedure. Per ottenere queste informazioni, usare il [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) proprietà. Il **Execute** (metodo) non restituirà le informazioni corrette quando abbinata **adAsyncExecute**, semplicemente perché quando viene eseguito un comando in modo asincrono, il numero di record interessati non può ancora essere conosciuto al momento il metodo restituisce.  
  
 *Parametri*  
 Facoltativo. Oggetto **Variant** matrice di valori dei parametri usati in combinazione con la stringa di input o di un flusso specificato **CommandText** oppure **CommandStream**. (I parametri di output non restituisce i valori corretti quando viene passato in questo argomento).  
  
 *Opzioni*  
 Facoltativo. Oggetto **lungo** valore che indica come il provider deve valutare il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) o la [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) proprietà del [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto. Può essere un valore di maschera di bit effettuato utilizzando [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e/o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valori. Ad esempio, è possibile usare **adCmdText** e **adExecuteStream** in combinazione, se si desidera utilizzare ADO valutare il valore della **CommandText** proprietà come testo, e indica che il comando deve annullare e viene restituito alcun record che potrebbe essere generato quando viene eseguito il testo del comando.  
  
> [!NOTE]
>  Usare la **ExecuteOptionEnum** valore **adExecuteStream** per migliorare le prestazioni riducendo al minimo l'elaborazione interna. Se **adExecuteStream** è stato specificato, le opzioni **adAsyncFetch** e **adAsynchFetchNonBlocking** vengono ignorati. Non usare la **CommandTypeEnum** i valori di **adCmdFile** oppure **adCmdTableDirect** con **Execute**. Questi valori possono essere usati solo come opzioni con il [aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) metodi di una **Recordset**.  
  
## <a name="remarks"></a>Note  
 Usando il **Execute** metodo su un **comando** viene eseguito la query specificata nell'oggetto di **CommandText** proprietà o **CommandStream** proprietà dell'oggetto.  
  
 I risultati vengono restituiti un **Recordset** (per impostazione predefinita) o come un flusso di informazioni binarie. Per ottenere un flusso binario, specificare **adExecuteStream** nelle *opzioni*, quindi fornire un flusso impostando **Command.Properties ("Output Stream")**. Un oggetto ADO **Stream** oggetto può essere specificato per ricevere i risultati o un altro oggetto di flusso, ad esempio l'oggetto risposta IIS può essere specificato. Se è stato specificato alcun flusso prima di chiamare **Execute** con **adExecuteStream**, si verifica un errore. La posizione del flusso sul valore restituito da **Execute** è provider specifico.  
  
 Se il comando non può restituire risultati (ad esempio, una query di aggiornamento di SQL) restituisce il provider **Nothing** fino a quando l'opzione **adExecuteStream** è specificata; in caso contrario, il metodo Execute restituisce un chiuso **Recordset**. Alcune lingue dell'applicazione consentono di ignorare questo valore restituito se nessun **Recordset** desiderata.  
  
 **Eseguire** genera un errore se l'utente specifica un valore per **CommandStream** quando la **CommandType** viene **adCmdStoredProc**,  **adCmdTable**, oppure **adCmdTableDirect**.  
  
 Se la query include parametri, i valori corrente per il **comandi** vengono usati i parametri dell'oggetto a meno che non si esegue l'override di questi valori con i valori dei parametri passati con la **Execute** chiamare. È possibile eseguire l'override di un subset dei parametri omettendo i nuovi valori per alcuni dei parametri quando si chiama il **Execute** (metodo). L'ordine in cui si specificano i parametri è lo stesso ordine in cui li passa il metodo. Ad esempio, se sono presenti parametri quattro (o più) e si desidera passare i valori nuovi per solo il primo e il quarto parametro, passerebbe `Array(var1,,,var4)` come il *parametri* argomento.  
  
> [!NOTE]
>  I parametri di output non restituirà i valori corretti quando viene passato nel *parametri* argomento.  
  
 Un' [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento verrà generato quando l'operazione è terminata.  
  
> [!NOTE]
>  Esecuzione di comandi che contengono gli URL, quelle che usano lo schema http richiamerà automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Proprietà CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Eseguire il metodo (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
