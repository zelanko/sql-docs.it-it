---
title: Metodo Execute21 (RDS) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964207"
---
# <a name="execute21-method-rds"></a>Metodo Execute21 (Servizi Desktop remoto)
Esegue la richiesta e crea un recordset ADO da utilizzare in ADO 2,1.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa utilizzata per la connessione al provider OLE DB in cui verrà inviata la richiesta per l'esecuzione. Se un gestore viene specificato tramite *HandlerString*, può modificare o sostituire la stringa di connessione.  
  
 *HandlerString*  
 La stringa identifica il gestore da usare con questa esecuzione. La stringa contiene due parti. La prima parte contiene il nome (ProgID) del gestore da usare. La seconda parte della stringa contiene gli argomenti da passare al gestore. Il modo in cui la stringa arguments viene interpretata è un gestore specifico. Le due parti sono separate dalla prima istanza di una virgola nella stringa (sebbene la stringa degli argomenti possa contenere altre virgole). Gli argomenti sono facoltativi.  
  
 *QueryString*  
 Comando nel linguaggio di comando supportato dal provider OLE DB identificato nella stringa di connessione. Per i provider basati su SQL, potrebbe contenere un' [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione Command, ma per i provider non SQL (ad esempio, MSDataShape) potrebbe non essere un' [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione di query.  
  
 Inoltre, se viene utilizzato un gestore (ed è consigliabile utilizzare un gestore), il gestore può modificare o sostituire il valore specificato qui. Ad esempio, il gestore in genere sostituisce *QueryString* con una stringa di query dal relativo file ini. Per impostazione predefinita, viene usato il file msdfmap. ini.  
  
 *lMarshalOptions*  
 Consente di impostare le opzioni di marshalling sul set di righe o sul recordset restituito.  
  
 *TableID*  
 Variant di tipo VT_EMPTY o VT_BSTR. Se questo valore è di tipo VT_EMPTY, viene ignorato. Se è di tipo VT_BSTR, il recordset viene creato usando **adCmdTableDirect** usando il valore specificato qui e il parametro *QueryString* viene ignorato.  
  
 *lExecuteOptions*  
 Maschera di maschera delle opzioni di esecuzione:  
  
 1 =*ReadOnly* il recordset verrà aperto utilizzando **adLockReadOnly**.  
  
 2 =*nobatch* il recordset verrà aperto utilizzando **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* il chiamante garantisce che le informazioni sui parametri per tutti i parametri vengano fornite in *pParameters*.  
  
 8 = le informazioni sul parametro*GetInfo* per la query verranno ottenute dal provider OLE DB e restituite nel parametro *pParameters* . La query non viene eseguita e non viene restituito alcun recordset.  
  
 16 = GetHiddenColumns il recordset verrà aperto utilizzando **adLockBatchOptimistic** e tutte le colonne nascoste verranno incluse nel recordset.  
  
 Sebbene *ReadOnly*, *nobatch* e *GetHiddenColumns* siano opzioni che si escludono a vicenda, non è un errore impostare più di uno di essi. Se sono impostate più opzioni, *GetHiddenColumns* avrà la precedenza su tutte le altre opzioni, seguite da *ReadOnly*. Se non viene specificata alcuna opzione, per impostazione predefinita il recordset viene aperto utilizzando **adLockBatchOptimistic** ma le colonne nascoste non sono incluse nel recordset.  
  
 *pParameters*  
 Variant che contiene una matrice sicura di definizioni di parametri. Se l'opzione *GetInfo* è stata specificata in *lExecuteOptions*, questo parametro viene utilizzato per restituire le definizioni dei parametri ottenute dal provider OLE DB. In caso contrario, questo parametro può essere vuoto.  
  
## <a name="remarks"></a>Osservazioni  
 Il parametro *HandlerString* può essere null. Ciò che si verifica in questo caso dipende dalla modalità di configurazione del server RDS. Una stringa del gestore "MSDFMAP. handler" indica che deve essere usato il gestore fornito da Microsoft (msdfmap. dll). Una stringa del gestore "MASDFMAP. Handler, Sample. ini" indica che è necessario utilizzare il gestore msdfmap. dll e che l'argomento "Sample. ini" deve essere passato al gestore. MSDFMAP. dll interpreterà l'argomento come direzione per utilizzare Sample. ini per verificare le stringhe di connessione e di query.  
  
> [!NOTE]
>  Il metodo **Execute21** è una versione del [metodo Execute (RDS)](../../../ado/reference/rds-api/execute-method-rds.md). Quando è necessario usare il metodo **Execute** per comunicare con ADO 2,1, è possibile chiamare il metodo **Execute21** . Le funzionalità del metodo **Execute** in ADO 2,5 e versioni successive sono un superset delle funzionalità fornite per lo stesso metodo in ADO 2,1.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


