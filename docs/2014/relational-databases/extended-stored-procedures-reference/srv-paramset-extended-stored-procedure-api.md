---
title: srv_paramset (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramset
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 00645f619a89010bb4e2b112d50e00cbc6f40dce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127152"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Imposta il valore di un parametro restituito di chiamata a una stored procedure remota. Questa funzione è stata sostituita dalla funzione **srv_paramsetoutput**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. In questo caso, l'handle che ha ricevuto la chiamata alla stored procedure remota. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *n*  
 Indica il numero del parametro da impostare. Il primo parametro è 1.  
  
 *data*  
 Puntatore al valore dei dati da inviare di nuovo al client come parametro restituito della stored procedure remota.  
  
 *Len*  
 Specifica la lunghezza effettiva dei dati da restituire. Se il tipo di dati del parametro ha una lunghezza costante e non consente valori Null (ad esempio, *srvbit* o *srvint1*), *len* viene ignorato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED se il valore del parametro è stato impostato correttamente; in caso contrario, FAIL. Restituisce FAIL se non esiste una stored procedure remota corrente, se non è presente il parametro *n* della stored procedure remota, se il parametro non è un parametro restituito o se l'argomento *len* non è valido.  
  
 Se *len* è 0, restituisce NULL. L'impostazione di *len* su 0 è l'unico modo per restituire NULL al client.  
  
 Questa funzione restituisce i valori seguenti, se il parametro è uno dei [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tipi di dati.  
  
|Nuovi tipi di dati|Lunghezza dei dati restituiti|  
|--------------------|------------------------|  
|`BITN`|**Null:** *Len* = 0, dati = IG, RET = 0<br /><br /> **Zero:** N/A<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|`BIGVARCHAR`|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGCHAR`|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGBINARY`|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGVARBINARY`|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|NCHAR|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|NVARCHAR|**Null:** *Len* = 0, dati = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = valido, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`NTEXT`|**Null:** *Len* = IG, data = IG, RET = 0<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = IG, data = IG, RET = 0<br /><br /> 255: *Len* = IG, data = IG, RET = 0 ** \<**|  
|RET = valore restituito di srv_paramset||  
|IG = il valore verrà ignorato||  
|valid = qualsiasi puntatore valido ai dati||  
  
## <a name="remarks"></a>Osservazioni  
 I parametri contengono i dati passati tra i client e l'applicazione con stored procedure remote. Il client può specificare determinati parametri come parametri restituiti. Questi parametri restituiti possono contenere valori che l'applicazione del server Open Data Services passa nuovamente al client. L'utilizzo di parametri restituiti è analogo al passaggio di parametri per riferimento.  
  
 Non è possibile impostare il valore restituito per un parametro non richiamato come parametro restituito. È possibile usare **srv_paramstatus** per determinare la modalità di richiamo del parametro.  
  
 Questa funzione imposta il valore restituito per un parametro ma non lo invia effettivamente al client. Tutti i parametri restituiti, indipendentemente dal fatto che i relativi valori restituiti siano stati impostati con **srv_paramset**, vengono inviati automaticamente al client quando **srv_senddone** viene chiamato con il flag di stato SRV_DONE_FINAL impostato.  
  
 Quando viene effettuata una chiamata a una stored procedure remota con parametri, tali parametri possono essere passati per nome o per posizione (senza nome). Se invece viene effettuata con alcuni parametri passati per nome e altri passati per posizione, si verifica un errore. Il gestore SRV_RPC viene comunque chiamato, ma risulta che non sono presenti parametri e **srv_rpcparams** restituisce 0.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_paramsetoutput &#40;API stored procedure estesa&#41;](srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
