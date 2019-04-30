---
title: Metodo (ADO Stream) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0df165514a10bc667c8bd2cc6d2a8569faa79d11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239710"
---
# <a name="open-method-ado-stream"></a>Metodo Open (Stream - ADO)
Consente di aprire una [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto per gestire i flussi di dati binari o testo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **Variant** valore che specifica l'origine dei dati per il **Stream**. *Origine* può contenere una stringa URL assoluto che punta a un nodo esistente in una struttura ad albero ben noti, ad esempio un sistema di posta elettronica o un file. Un URL deve essere specificato usando la parola chiave URL ("URL =*combinazione*://*server*/*cartella*"). In alternativa *origine* può contenere un riferimento a un a cui è già aperta [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto, che viene aperto il flusso predefinito associato il **Record**. Se *origine* non viene specificato, un **Stream** viene creata e aperta, associata a Nessuna origine sottostante per impostazione predefinita. Per altre informazioni sugli schemi URL e i provider associati, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Mode*  
 Facoltativo. Oggetto [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valore che specifica la modalità di accesso per i risultanti **Stream** (ad esempio, di lettura/scrittura o sola lettura). Valore predefinito è **adModeUnknown**. Vedere le [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà per altre informazioni sulle modalità di accesso. Se *modalità* non viene specificato, viene ereditato dall'oggetto di origine. Ad esempio, se l'origine **Record** viene aperto in modalità di sola lettura, il **Stream** verrà inoltre aperta in modalità di sola lettura per impostazione predefinita.  
  
 *OpenOptions*  
 Facoltativo. Oggetto [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) valore. Valore predefinito è **adOpenStreamUnspecified**.  
  
 *UserName*  
 Facoltativo. Oggetto **stringa** valore contenente l'ID utente che, se necessario, accede il **Stream** oggetto.  
  
 *Password*  
 Facoltativo. Oggetto **stringa** valore contenente la password, se necessario, accederà il **Stream** oggetto.  
  
## <a name="remarks"></a>Note  
 Quando un **Record** oggetto viene passato come parametro di origine, il *UserID* e *Password* parametri non vengono utilizzati perché l'accesso al **Record** l'oggetto è già disponibile. Allo stesso modo, il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) delle **Record** oggetto viene trasferito al **Stream** oggetto. Quando *origine* non viene specificato, il **Stream** aperto non contiene dati e dispone di un [dimensioni](../../../ado/reference/ado-api/size-property-ado-stream.md) pari a zero (0). Per evitare la perdita di dati che viene scritto in questo **Stream** quando il **Stream** viene chiusa, salvare il **Stream** con il [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) o[ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) metodi, o salvarlo in un'altra posizione di memoria.  
  
 Un' *OpenOptions* pari a **adOpenStreamFromRecord** identifica il contenuto del *origine* parametro sia una è già aperta **Record**oggetto. Il comportamento predefinito consiste nel considerare *origine* sotto forma di URL che punta direttamente a un nodo in una struttura ad albero, ad esempio un file. Viene aperto il flusso predefinito associato a tale nodo.  
  
 Mentre il **Stream** è non è aperto, è possibile leggere tutte le proprietà di sola lettura delle **Stream**. Se un **Stream** viene aperto in modo asincrono, tutte le operazioni successive (diverso da controllare il [stato](../../../ado/reference/ado-api/state-property-ado.md) e altre proprietà di sola lettura) sono bloccati fino a quando il **Open** operazione completata.  
  
 Oltre alle opzioni che sono state illustrate in precedenza, non specificando *origine*, è possibile creare un'istanza di un **Stream** oggetto in memoria senza associarla a un'origine sottostante. È possibile aggiungere in modo dinamico i dati nel flusso scrivendo i dati binari o di testo per il **Stream** con [scrivere](../../../ado/reference/ado-api/write-method.md) oppure [WriteText](../../../ado/reference/ado-api/writetext-method.md), oppure caricando i dati da un file con [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Esempio di metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Metodo SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
