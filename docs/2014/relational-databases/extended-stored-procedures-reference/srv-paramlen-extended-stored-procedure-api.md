---
title: srv_paramlen (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramlen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2c858d0fa8579aff288efd7026ab4b65035bad8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127198"
---
# <a name="srv_paramlen-extended-stored-procedure-api"></a>srv_paramlen (API delle stored procedure estese)
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
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
  
 Questa funzione restituisce i valori seguenti, se il parametro è uno dei tipi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] dati di sistema seguenti.  
  
|Nuovi tipi di dati|Lunghezza dei dati di input|  
|--------------------|-----------------------|  
|`BITN`|**Null:** 1<br /><br /> **Zero:** 1<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|`BIGVARCHAR`|**Null:** 0<br /><br /> **Zero:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** *Len* effettivo|  
|`BIGCHAR`|**Null:** 0<br /><br /> **Zero:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`BIGBINARY`|**Null:** 0<br /><br /> **Zero:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`BIGVARBINARY`|**Null:** 0<br /><br /> **Zero:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** *Len* effettivo|  
|`NCHAR`|**Null:** 0<br /><br /> **Zero:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`NVARCHAR`|**Null:** 0<br /><br /> **Zero:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** *Len* effettivo|  
|`NTEXT`|**Null:** -1<br /><br /> **Zero:** -1<br /><br /> **>= 255:** -1<br /><br /> **<255:** -1|  
  
 \**Len* effettivo = lunghezza della stringa di caratteri multibyte  
  
## <a name="remarks"></a>Osservazioni  
 Ogni parametro di stored procedure remota ha una lunghezza massima e una lunghezza effettiva dei dati. Per i tipi di dati a lunghezza fissa standard che non consentono valori Null, le due lunghezze coincidono. Per i tipi di dati a lunghezza variabile, le lunghezze possono essere diverse. Un parametro dichiarato come `varchar(30)`, ad esempio, può includere dati con lunghezza pari solo a 10 byte. La lunghezza effettiva del parametro è 10, mentre la lunghezza massima è 30. La funzione **srv_paramlen** ottiene la lunghezza effettiva dei dati in byte di una stored procedure remota. Per ottenere la lunghezza massima dei dati di un parametro, usare **srv_parammaxlen**.  
  
 Quando viene effettuata una chiamata a una stored procedure remota con parametri, tali parametri possono essere passati per nome o per posizione (senza nome). Se invece viene effettuata con alcuni parametri passati per nome e altri passati per posizione, si verifica un errore. Il gestore SRV_RPC viene ancora chiamato, ma sembra che non siano presenti parametri e **srv_rpcparams** restituisce 0.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_paraminfo &#40;API stored procedure estesa&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API stored procedure estesa&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
