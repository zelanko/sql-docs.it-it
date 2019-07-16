---
title: Metodo Execute21 (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8434345dcc4436865e4981a19ef1164d35a852f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964207"
---
# <a name="execute21-method-rds"></a>Metodo Execute21 (Servizi Desktop remoto)
Esegue la richiesta e crea un recordset ADO per l'utilizzo in ADO 2.1.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa utilizzata per la connessione al provider OLE DB in cui verrà inviata la richiesta per l'esecuzione. Se viene specificato con un gestore *HandlerString*, è possibile modificare o sostituire la stringa di connessione.  
  
 *HandlerString*  
 La stringa identifica il gestore da utilizzare con questa esecuzione. La stringa contiene due parti. La prima parte contiene il nome (ProgID) del gestore da utilizzare. La seconda parte della stringa contiene argomenti da passare al gestore. Come viene interpretata la stringa di argomenti è gestore specifico. Le due parti sono separate dall'istanza prima della virgola nella stringa di (anche se la stringa di argomenti può contenere virgole aggiuntive). Gli argomenti sono facoltativi.  
  
 *QueryString*  
 Un comando nel linguaggio di comando supportato dal provider OLE DB identificato nella stringa di connessione. Per i provider basato su SQL, è possibile che contenga una [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione di comando, ma per i provider non SQL (ad esempio, MSDataShape) potrebbe non essere un [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione della query.  
  
 Inoltre, se un gestore di è in uso e si consiglia vivamente che un gestore di è utilizzabile, il gestore può modificare o sostituire il valore specificato qui. Ad esempio, in genere sostituisce il gestore *QueryString* con una stringa di query dal file ini. Per impostazione predefinita, il file MSDFMAP viene usato.  
  
 *lMarshalOptions*  
 Utilizzato per impostare le opzioni di marshalling nel set di righe/recordset restituito.  
  
 *TableID*  
 Una variante di tipo VT_EMPTY o VT_BSTR. Se questo valore è di tipo VT_EMPTY, viene ignorato. Se è di tipo VT_BSTR, il set di record viene creato usando **adCmdTableDirect** usando il valore specificato qui e il *QueryString* parametro viene ignorato.  
  
 *lExecuteOptions*  
 Maschera di bit delle opzioni di esecuzione:  
  
 1 =*ReadOnly* verrà aperta usando il set di record **adLockReadOnly**.  
  
 2 =*NoBatch* verrà aperta usando il set di record **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* il chiamante garantisce che le informazioni sui parametri per tutti i parametri viene fornite nel *pParameters*.  
  
 8 =*GetInfo* informazioni sui parametri per la query verrà ottenuti dal provider OLE DB e restituite nel *pParameters* parametro. La query non viene eseguita e non viene restituito alcun oggetto recordset.  
  
 16 = GetHiddenColumns verrà aperta usando il recordset **adLockBatchOptimistic** e le colonne nascoste verranno incluso nel set di record.  
  
 Sebbene *ReadOnly*, *NoBatch* e *GetHiddenColumns* si escludono a vicenda, non è corretto impostare più di uno di essi. Se sono impostate più opzioni, *GetHiddenColumns* ha la precedenza su tutte le altre opzioni, seguiti da *ReadOnly*. Se viene specificata alcuna opzione, per impostazione predefinita, viene aperto con il set di record **adLockBatchOptimistic** ma le colonne nascoste non vengono inclusi nel set di record.  
  
 *pParameters*  
 Una variante che contiene una matrice protetta di definizioni di parametro. Se il *GetInfo* opzione è stata specificata *lExecuteOptions*, questo parametro viene utilizzato per restituire le definizioni di parametro ottenute dal provider OLE DB. In caso contrario, questo parametro può essere vuoto.  
  
## <a name="remarks"></a>Note  
 Il *HandlerString* parametro può essere null. Ciò che accade in questo caso dipende dal modo in cui il server di servizi desktop remoto è configurato. Nome di un gestore di "MSDFMAP. Handler" indica che il gestore di Microsoft fornito (Msdfmap.dll) deve essere utilizzato. Nome di un gestore di "MASDFMAP.handler,sample.ini" indica che il gestore Msdfmap.dll deve essere utilizzato e che l'argomento "il file" deve essere passato al gestore. MSDFMAP.dll interpreterà l'argomento come una direzione da utilizzare il file per controllare le stringhe di connessione e la query.  
  
> [!NOTE]
>  Il **Execute21** metodo è una versione del [eseguire il metodo (RDS)](../../../ado/reference/rds-api/execute-method-rds.md). In cui è necessario usare il **Execute** metodo per comunicare con ADO 2.1, il **Execute21** metodo può essere invece chiamato. Le funzionalità dei **Execute** metodo in ADO 2.5 e versioni successiva sono un soprainsieme delle funzionalità fornito per il metodo di stesso in ADO 2.1.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


