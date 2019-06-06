---
title: Eseguire il metodo (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5c0fa79bdf5acc89b7d884afa604ab08e926d9e1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707703"
---
# <a name="execute-method-rds"></a>Metodo Execute (Servizi Desktop remoto)
Esegue la richiesta e crea un recordset ADO per l'utilizzo in ADO 2.5 e versioni successive.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa utilizzata per la connessione al provider OLE DB in cui verrà inviata la richiesta per l'esecuzione. Se viene specificato con un gestore *HandlerString* può modificare o sostituire la stringa di connessione.  
  
 *HandlerString*  
 Una stringa di due parti che identifica il gestore da utilizzare con questa esecuzione. La stringa contiene due parti. La prima parte contiene il nome (ProgID) del gestore da utilizzare. La seconda parte contiene argomenti da passare al gestore. I dettagli di come viene interpretata la stringa di argomenti sono specifici per ogni gestore. Le due parti sono separate per la prima istanza di una virgola nella stringa. La stringa di argomenti può contenere virgole aggiuntive. Gli argomenti sono facoltativi.  
  
 *QueryString*  
 Un comando nel linguaggio di comando supportato dal provider OLE DB identificato nella stringa di connessione. Per i provider basato su SQL *QueryString* può contenere un'istruzione di comando Transact-SQL, ma per i provider non SQL (ad esempio, MSDataShape) potrebbe non essere un [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione della query.  
  
 Se un gestore di è in uso, il gestore di è possibile modificare o sostituire il valore specificato qui. Ad esempio, in genere sostituisce il gestore *QueryString* con una stringa di query dal file ini. Per impostazione predefinita, il file MSDFMAP viene usato.  
  
 *lFetchOptions*  
 Indica il tipo di recupero asincrono.  
  
 Per altre informazioni, vedere [proprietà FetchOptions (Servizi Desktop remoto)](../../../ado/reference/rds-api/fetchoptions-property-rds.md).  
  
 *TableID*  
 Oggetto **Variant** di tipo VT_EMPTY o VT_BSTR. Se questo valore è di tipo VT_EMPTY, viene ignorato. Se è di tipo VT_BSTR, il set di record viene creato usando **adCmdTableDirect** e il valore specificato qui e il *QueryString* parametro viene ignorato.  
  
 *lExecuteOptions*  
 Una maschera di bit delle opzioni di esecuzione:  
  
 1 =*ReadOnly* verrà aperta usando il set di record **adLockReadOnly**.  
  
 2 =*NoBatch* verrà aperta usando il set di record **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* il chiamante garantisce che le informazioni sui parametri per tutti i parametri viene fornite nel *pParameters*.  
  
 8 =*GetInfo* informazioni sui parametri per la query verrà ottenuti dal provider OLE DB e restituite nel *pParameters* parametro. La query non viene eseguita e non viene restituito alcun oggetto recordset.  
  
 16 =*GetHiddenColumns* verrà aperta usando il set di record **adLockBatchOptimistic** e le colonne nascoste verranno incluso nel set di record.  
  
 *ReadOnly*, *NoBatch* e *GetHiddenColumns* si escludono a vicenda; tuttavia, non genera un errore per impostare più di uno di essi. Se sono impostate più opzioni, *GetHiddenColumns* ha la precedenza su tutte le altre, seguito da *ReadOnly*. Se viene specificata alcuna opzione, per impostazione predefinita, viene aperto con il set di record **adLockBatchOptimistic** e le colonne nascoste non sono incluse nel set di record.  
  
 *pParameters*  
 Oggetto **Variant** che contiene una matrice protetta di definizioni di parametro. Se il *GetInfo* opzione è stata specificata *lExecuteOptions*, questo parametro viene utilizzato per restituire le definizioni di parametro ottenute dal provider OLE DB. In caso contrario, questo parametro può essere vuoto.  
  
 *lcid*  
 L'identificatore LCID utilizzato per compilare gli eventuali errori che vengono restituiti in *pInformation*.  
  
 *pInformation*  
 Puntatore al messaggio di errore informativo restituito da Execute. Se NULL, viene restituita alcuna informazione di errore.  
  
## <a name="remarks"></a>Note  
 Il *HandlerString* parametro può essere null. Cosa accade in questo caso dipende dal modo in cui il server di servizi desktop remoto è configurato. Nome di un gestore di "MSDFMAP. Handler" indica che il gestore di Microsoft fornito (Msdfmap.dll) deve essere utilizzato. Nome di un gestore di "MASDFMAP.handler,sample.ini" indica che il gestore Msdfmap.dll deve essere utilizzato e che l'argomento "il file" deve essere passato al gestore. MSDFMAP.dll interpreterà l'argomento come una direzione da utilizzare il file per controllare le stringhe di connessione e la query.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


