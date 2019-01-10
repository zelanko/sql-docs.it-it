---
title: srv_parammaxlen (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_parammaxlen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_parammaxlen
ms.assetid: 49bfc29d-f76a-4963-b0e6-b8532dfda850
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7fadcfbc6249ca15ecd9581cc50d58d0e3a09a5d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360833"
---
# <a name="srvparammaxlen-extended-stored-procedure-api"></a>srv_parammaxlen (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce la lunghezza massima dei dati di un parametro di chiamata a una stored procedure remota. Questa funzione è stata sostituita dalla funzione **srv_paraminfo**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_parammaxlen (  
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
 Lunghezza massima in byte dei dati del parametro. Se non è presente nessun parametro *n* o nessuna stored procedure remota, restituisce -1.  
  
 Questa funzione restituisce i valori seguenti, se il parametro è uno dei tipi di dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguenti.  
  
|Nuovi tipi di dati|Lunghezza dei dati di input|  
|--------------------|-----------------------|  
|`BITN`|**NULL:** 1<br /><br /> **ZERO:** 1<br /><br /> **> = 255:** N/D<br /><br /> **< 255:** N/D|  
|`BIGVARCHAR`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`BIGCHAR`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`BIGBINARY`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`BIGVARBINARY`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`NCHAR`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`NVARCHAR`|**NULL:** 255<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`NTEXT`|**NULL:** -1<br /><br /> **ZERO:** -1<br /><br /> **>=255:** -1<br /><br /> **\<255:** -1|  
  
## <a name="remarks"></a>Note  
 Ogni parametro di stored procedure remota ha una lunghezza massima e una lunghezza effettiva dei dati. Per i tipi di dati a lunghezza fissa standard che non consentono valori Null, le due lunghezze coincidono. Per i tipi di dati a lunghezza variabile, le lunghezze possono essere diverse. Un parametro dichiarato come **varchar(30)** può ad esempio contenere dati con lunghezza pari a 10 byte. La lunghezza effettiva del parametro è 10, mentre la lunghezza massima è 30. La funzione **srv_parammaxlen** ottiene la lunghezza massima dei dati di una stored procedure remota. Per ottenere la lunghezza effettiva di un parametro, usare **srv_paramlen**.  
  
 Quando viene effettuata una chiamata a una stored procedure remota con parametri, tali parametri possono essere passati per nome o per posizione (senza nome). Se invece viene effettuata con alcuni parametri passati per nome e altri passati per posizione, si verifica un errore. Il gestore SRV_RPC viene comunque chiamato, ma risulta che non sono presenti parametri e **srv_rpcparams** restituisce 0.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_paraminfo &#40;API delle stored procedure estese&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API delle stored procedure estese&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
