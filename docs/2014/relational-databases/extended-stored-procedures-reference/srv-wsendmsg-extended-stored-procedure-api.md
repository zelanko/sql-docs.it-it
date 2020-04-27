---
title: srv_wsendmsg (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_wsendmsg
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 18b166472cff011b3766645dde61f562c766ff2c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63140453"
---
# <a name="srv_wsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Invia un messaggio Unicode al client.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *Msgnum*  
 Numero di messaggio a 4 byte.  
  
 *Gravità*  
 Specifica la gravità dell'errore. Un livello di gravità minore o uguale a 10 è considerato un messaggio informativo; in caso contrario, è un errore.  
  
 *message*  
 Puntatore alla stringa Unicode da inviare al client.  
  
 *msglen*  
 Specifica la lunghezza, espressa in caratteri, di *message*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare questa funzione per inviare messaggi in Unicode. È simile a **srv_sendmsg**, ma il messaggio che invia è una stringa WCHAR anziché una stringa di tipo DBCHAR. Notare che la lunghezza del messaggio viene riportata in caratteri anziché in byte e che *msglen* non sarà mai uguale a SRV_NULLTERM.  
  
 La funzione restituisce FAIL quando:  
  
-   Il valore *msglen* specificato non è incluso nell'intervallo 0-32242.  
  
-   Il valore *msglen* specificato è 0 ma il puntatore del messaggio è NULL.  
  
-   Si verifica un errore durante l'invio del messaggio di errore tramite rete.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedi anche  
 [srv_sendmsg &#40;API Stored procedure estesa&#41;](srv-sendmsg-extended-stored-procedure-api.md)  
  
  
