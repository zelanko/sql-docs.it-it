---
title: srv_paramlen (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramlen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c89a9ddc1020f29bbcd661ec4c9672ba37f7770
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005708"
---
# <a name="srvparamlen-extended-stored-procedure-api"></a>srv_paramlen (API delle stored procedure estese)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce la lunghezza dei dati di un parametro di chiamata a una stored procedure remota. Questa funzione è stata sostituita dalla funzione **srv_paraminfo**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_paramlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. In questo caso, l'handle che ha ricevuto la chiamata alla stored procedure remota. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *n*  
 Indica il numero del parametro. Il primo parametro è 1.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Lunghezza effettiva in byte dei dati del parametro. Se non è presente nessun parametro *n* o nessuna stored procedure remota, restituisce -1. Se il parametro *n* è NULL, restituisce 0.  
  
 Questa funzione restituisce i valori seguenti, se il parametro è uno dei seguenti tipi di dati di sistema di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
|Nuovi tipi di dati|Lunghezza dei dati di input|  
|--------------------|-----------------------|  
|**BITN**|**NULL:** 1<br /><br /> **ZERO:** 1<br /><br /> **>=255:** N/D<br /><br /> **<255:** N/D|  
|**BIGVARCHAR**|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **>=255:** 255<br /><br /> **<255:** valore *len* effettivo|  
|**BIGCHAR**|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGBINARY**|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGVARBINARY**|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **>=255:** 255<br /><br /> **<255:** valore *len* effettivo|  
|**NCHAR**|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**NVARCHAR**|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **>=255:** 255<br /><br /> **<255:** valore *len* effettivo|  
|**NTEXT**|**NULL:** -1<br /><br /> **ZERO:** -1<br /><br /> **>=255:** -1<br /><br /> **\<255:** -1|  
  
 \*   Valore *len* effettivo = Lunghezza della stringa di carattere multibyte (cch)  
  
## <a name="remarks"></a>Remarks  
 Ogni parametro di stored procedure remota ha una lunghezza massima e una lunghezza effettiva dei dati. Per i tipi di dati a lunghezza fissa standard che non consentono valori Null, le due lunghezze coincidono. Per i tipi di dati a lunghezza variabile, le lunghezze possono essere diverse. Un parametro dichiarato come **varchar(30)** può ad esempio contenere dati con lunghezza pari a 10 byte. La lunghezza effettiva del parametro è 10, mentre la lunghezza massima è 30. La funzione **srv_paramlen** ottiene la lunghezza effettiva dei dati in byte di una stored procedure remota. Per ottenere la lunghezza massima dei dati di un parametro, usare **srv_parammaxlen**.  
  
 Quando viene effettuata una chiamata a una stored procedure remota con parametri, tali parametri possono essere passati per nome o per posizione (senza nome). Se invece viene effettuata con alcuni parametri passati per nome e altri passati per posizione, si verifica un errore. Il gestore SRV_RPC viene comunque chiamato, ma risulta che non sono presenti parametri e **srv_rpcparams** restituisce 0.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_paraminfo &#40;API delle stored procedure estese&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API delle stored procedure estese&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
