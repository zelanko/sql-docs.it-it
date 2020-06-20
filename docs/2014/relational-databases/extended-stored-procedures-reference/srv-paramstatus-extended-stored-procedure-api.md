---
title: srv_paramstatus (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramstatus
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramstatus
ms.assetid: 86cecd45-0b09-42e9-8152-32a12a1c2b7a
author: rothja
ms.author: jroth
ms.openlocfilehash: c7b67464e8866697b0234af46bf2e773071c73ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050655"
---
# <a name="srv_paramstatus-extended-stored-procedure-api"></a>srv_paramstatus (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce lo stato di un determinato parametro di chiamata a una stored procedure remota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_paramstatus (  
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
  
## <a name="returns"></a>Restituisce  
 `int` contenente flag di stato per il parametro. Attualmente è disponibile un solo flag: se il bit 0 è impostato su 1, il parametro è un parametro restituito. Se non è presente nessun parametro *n* o nessuna stored procedure remota, restituisce -1.  
  
## <a name="remarks"></a>Osservazioni  
 Questa routine restituisce i flag di stato per un determinato parametro di chiamata a una stored procedure remota.  
  
 I parametri contengono i dati passati tra i client e l'applicazione con stored procedure remote. Il client può specificare determinati parametri come parametri restituiti. Questi parametri restituiti possono contenere valori che l'applicazione passa nuovamente al client.  
  
 Attualmente l'unico flag di stato è quello che indica se il parametro è un parametro restituito.  
  
 Quando viene effettuata una chiamata a una stored procedure remota con parametri, tali parametri possono essere passati per nome o per posizione (senza nome). Se invece viene effettuata con alcuni parametri passati per nome e altri passati per posizione, si verifica un errore. Se si verifica un errore, il gestore SRV_RPC viene ancora chiamato, ma viene visualizzato come se non fossero presenti parametri e **srv_rpcparams** restituisce 0.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_rpcparams &#40;API delle stored procedure estese&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
