---
title: Metodo Open (recordset ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a091a606cf3049c055794bc16cc51db78a40978
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762179"
---
# <a name="open-method-ado-recordset"></a>Metodo Open (Recordset - ADO)
Apre un cursore su un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *origine*  
 Facoltativa. **Variante** che restituisce un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) valido, un'istruzione SQL, un nome di tabella, una chiamata stored procedure, un URL o il nome di un file o di un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) contenente un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)archiviato in modo permanente.  
  
 *ActiveConnection*  
 Facoltativa. **Variant** che restituisce un nome di variabile oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) valido o una **stringa** che contiene parametri [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .  
  
 *CursorType*  
 Facoltativa. Valore [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) che determina il tipo di cursore che il provider deve utilizzare per l'apertura del **Recordset**. Il valore predefinito è **adOpenForwardOnly**.  
  
 *LockType*  
 Facoltativa. Valore [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) che determina il tipo di blocco (concorrenza) che il provider deve utilizzare per l'apertura del **Recordset**. Il valore predefinito è **adLockReadOnly**.  
  
 *Opzioni*  
 Facoltativa. Valore **Long** che indica il modo in cui il provider deve valutare l'argomento di *origine* se rappresenta un oggetto diverso da un oggetto **Command** oppure se il **Recordset** deve essere ripristinato da un file in cui è stato salvato in precedenza. Può essere uno o più valori [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) , che possono essere combinati con un operatore OR bit per bit.  
  
> [!NOTE]
>  Se si apre un **Recordset** da un **flusso** contenente un **Recordset**salvato in modo permanente, l'utilizzo di un valore [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) di **adAsyncFetchNonBlocking** non avrà alcun effetto; il recupero sarà sincrono e bloccante.  
  
> [!NOTE]
>  I valori **ExecuteOpenEnum** di **adExecuteNoRecords** o **adExecuteStream** non devono essere utilizzati con **Open**.  
  
## <a name="remarks"></a>Osservazioni  
 Il cursore predefinito per un **Recordset** ADO è un cursore di sola lettura di sola trasmissione che si trova nel server.  
  
 Utilizzando il metodo **Open** su un oggetto **Recordset** , viene aperto un cursore che rappresenta i record di una tabella di base, i risultati di una query o un **Recordset**salvato in precedenza.  
  
 Utilizzare l'argomento di *origine* facoltativo per specificare un'origine dati utilizzando uno dei seguenti elementi: una variabile oggetto **comando** , un'istruzione SQL, un stored procedure, un nome di tabella, un URL o un nome di percorso file completo. Se l' *origine* è un nome di percorso del file, può essere un percorso completo ("c:\dir\file.RST"), un percorso relativo ("... \File.RST ") o un URL (" <https://files/file.rst> ").  
  
 Non è consigliabile usare l'argomento di *origine* del metodo **Open** per eseguire una query di azione che non restituisce record perché non esiste un modo semplice per determinare se la chiamata ha avuto esito positivo. Il **Recordset** restituito da tale query verrà chiuso. Per eseguire una query che non restituisce record, ad esempio un'istruzione SQL INSERT, chiamare invece il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) di un oggetto **Command** o il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) di un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
 L'argomento *ActiveConnection* corrisponde alla proprietà [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) e specifica in quale connessione aprire l'oggetto **Recordset** . Se si passa una definizione di connessione per questo argomento, ADO apre una nuova connessione usando i parametri specificati. Dopo aver aperto il **Recordset** con un cursore sul lato client impostando la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) su **adUseClient**, è possibile modificare il valore di questa proprietà per inviare aggiornamenti a un altro provider. In alternativa, è possibile impostare questa proprietà su **Nothing** (in Microsoft Visual Basic) o su null per disconnettere il **Recordset** da qualsiasi provider. Tuttavia, la modifica di *ActiveConnection* per un cursore sul lato server genera un errore.  
  
 Per gli altri argomenti che corrispondono direttamente alle proprietà di un oggetto **Recordset** (*source*, *CursorType*e *LockType*), la relazione degli argomenti con le proprietà è la seguente:  
  
-   La proprietà è di lettura/scrittura prima dell'apertura dell'oggetto **Recordset** .  
  
-   Le impostazioni delle proprietà vengono usate a meno che non si passino gli argomenti corrispondenti durante l'esecuzione del metodo **Open** . Se si passa un argomento, viene eseguito l'override dell'impostazione della proprietà corrispondente e l'impostazione della proprietà viene aggiornata con il valore dell'argomento.  
  
-   Dopo aver aperto l'oggetto **Recordset** , queste proprietà diventano di sola lettura.  
  
> [!NOTE]
>  La proprietà **ActiveConnection** è di sola lettura per gli oggetti **Recordset** la cui proprietà [source](../../../ado/reference/ado-api/source-property-ado-recordset.md) è impostata su un oggetto **Command** valido, anche se l'oggetto **Recordset** non è aperto.  
  
 Se si passa un oggetto **Command** nell'argomento *source* e si passa anche un argomento *ActiveConnection* , si verificherà un errore. La proprietà **ActiveConnection** dell'oggetto **Command** deve essere già impostata su un oggetto **connessione** o una stringa di connessione valida.  
  
 Se si passa un valore diverso da un oggetto **Command** nell'argomento di *origine* , è possibile usare l'argomento *options* per ottimizzare la valutazione dell'argomento di *origine* . Se l'argomento *options* non è definito, è possibile che si verifichi un calo delle prestazioni perché ADO deve effettuare chiamate al provider per determinare se l'argomento è un'istruzione SQL, un stored procedure, un URL o un nome di tabella. Se si conosce il tipo di *origine* utilizzato, l'impostazione dell'argomento *options* indica a ADO di passare direttamente al codice pertinente. Se l'argomento *options* non corrisponde al tipo di *origine* , si verificherà un errore.  
  
 Se si passa un oggetto **flusso** nell'argomento di *origine* , non è necessario passare informazioni negli altri argomenti. In caso contrario, verrà generato un errore. Le informazioni **ActiveConnection** non vengono mantenute quando un **Recordset** viene aperto da un **flusso**.  
  
 Il valore predefinito per l'argomento *options* è **AdCmdFile** se al **Recordset**non è associata alcuna connessione. Questa situazione si verifica in genere per gli oggetti **Recordset** archiviati in modo permanente.  
  
 Se l'origine dati non restituisce record, il provider imposta entrambe le proprietà [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) su **true**e la posizione del record corrente non è definita. È comunque possibile aggiungere nuovi dati a questo oggetto **Recordset** vuoto se il tipo di cursore lo consente.  
  
 Una volta terminate le operazioni su un oggetto **Recordset** aperto, utilizzare il metodo [Close](../../../ado/reference/ado-api/close-method-ado.md) per liberare tutte le risorse di sistema associate. La chiusura di un oggetto non comporta la rimozione dalla memoria; è possibile modificare le impostazioni delle proprietà e usare il metodo **Open** per aprirlo di nuovo in un secondo momento. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto su *Nothing*.  
  
 Prima di impostare la proprietà **ActiveConnection** , chiamare **Open** senza operandi per creare un'istanza di un **Recordset** creato accodando campi alla raccolta di [campi](../../../ado/reference/ado-api/fields-collection-ado.md) del **Recordset** .  
  
 Se è stata impostata la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) su **adUseClient**, è possibile recuperare le righe in modo asincrono in uno dei due modi. Il metodo consigliato consiste nell'impostare le *Opzioni* su **adAsyncFetch**. In alternativa, è possibile utilizzare la proprietà dinamica "elaborazione del set di righe asincrono" nella raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) , ma gli eventi recuperati correlati possono essere persi se non si imposta il parametro *options* su **adAsyncFetch**.  
  
> [!NOTE]
>  Il recupero in background in MS Remote Provider è supportato solo tramite il parametro *options* del metodo **Open** .  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Alcune combinazioni di valori [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) non sono valide. Per informazioni sulle opzioni che non possono essere combinate, vedere gli argomenti relativi a [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Esempio di metodi Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Esempio di metodi Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Esempio di metodi Save e Open (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
