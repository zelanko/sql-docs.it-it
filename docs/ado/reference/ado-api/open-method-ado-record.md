---
description: Metodo Open (Record - ADO)
title: Metodo Open (record ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ad606821e423892d49feb49a0920c7aea9056aa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990342"
---
# <a name="open-method-ado-record"></a>Metodo Open (Record - ADO)
Apre un oggetto [record](./record-object-ado.md) esistente o crea un nuovo elemento rappresentato dal **record**, ad esempio un file o una directory.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativa. **Variant** che può rappresentare l'URL dell'entità che deve essere rappresentata da questo oggetto **record** , un **comando**, un [Recordset](./recordset-object-ado.md) aperto o un altro oggetto **record** , una stringa che contiene un'istruzione SQL SELECT o un nome di tabella.  
  
 *ActiveConnection*  
 Facoltativa. **Variant** che rappresenta la stringa di connessione o l'oggetto [connessione](./connection-object-ado.md) aperta.  
  
 *Modalità*  
 Facoltativa. Valore [ConnectModeEnum](./connectmodeenum.md) che specifica la modalità di accesso per l'oggetto **record** risultante. Il valore predefinito è **adModeUnknown**.  
  
 *CreateOptions*  
 Facoltativa. Valore [RecordCreateOptionsEnum](./recordcreateoptionsenum.md) che specifica se deve essere aperto un file o una directory esistente oppure se è necessario creare un nuovo file o una nuova directory. Il valore predefinito è **adFailIfNotExists**. Se è impostato sul valore predefinito, la modalità di accesso viene ottenuta dalla proprietà [mode](./mode-property-ado.md) . Questo parametro viene ignorato quando il parametro di *origine* non contiene un URL.  
  
 *Opzioni*  
 Facoltativa. Valore [RecordOpenOptionsEnum](./recordopenoptionsenum.md) che specifica le opzioni per l'apertura del **record**. Il valore predefinito è **adOpenRecordUnspecified**. Questi valori possono essere combinati.  
  
 *UserName*  
 Facoltativa. Valore **stringa** che contiene l'ID utente che, se necessario, autorizza l'accesso all' *origine*.  
  
 *Password*  
 Facoltativa. Valore **stringa** che contiene la password che, se necessaria, verifica il *nome utente*.  
  
## <a name="remarks"></a>Osservazioni  
 Il *codice sorgente* può essere:  
  
-   Un URL. Se il protocollo per l'URL è http, il provider Internet verrà richiamato per impostazione predefinita. Se l'URL punta a un nodo che contiene uno script eseguibile, ad esempio. Pagina ASP), per impostazione predefinita viene aperto un **record** che contiene l'origine anziché il contenuto eseguito. Usare l'argomento *options* per modificare questo comportamento.  
  
-   Oggetto **record** . Un oggetto **record** aperto da un altro **record** Clona l'oggetto **record** originale.  
  
-   Oggetto **Command** . L'oggetto **record** aperto rappresenta la singola riga restituita dall'esecuzione del **comando**. Se i risultati contengono più di una riga, il contenuto della prima riga viene inserito nel record ed è possibile che venga aggiunto un errore alla raccolta **Errors** .  
  
-   Istruzione SQL SELECT. L'oggetto **record** aperto rappresenta la singola riga restituita eseguendo il contenuto della stringa. Se i risultati contengono più di una riga, il contenuto della prima riga viene inserito nel record ed è possibile che venga aggiunto un errore alla raccolta **Errors** .  
  
-   Nome della tabella.  
  
 Se l'oggetto **record** rappresenta un'entità a cui non è possibile accedere con un URL (ad esempio, una riga di un **Recordset** derivato da un database), i valori della proprietà [ParentURL](./parenturl-property-ado.md) e del campo a cui si accede con la costante **adRecordURL** sono null.  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (connessione ADO)](./open-method-ado-connection.md)   
 [Metodo Open (recordset ADO)](./open-method-ado-recordset.md)   
 [Metodo Open (flusso ADO)](./open-method-ado-stream.md)   
 [Metodo OpenSchema](./openschema-method.md)