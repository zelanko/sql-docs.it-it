---
title: srv_rpcdb (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcdb
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9cb924bbaa93322a93d77d4a5e1234ba95d4324a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472078"
---
# <a name="srvrpcdb-extended-stored-procedure-api"></a>srv_rpcdb (API delle stored procedure estese)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce il componente del nome del database per la stored procedure remota corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *len*  
 Puntatore a una variabile **int** che riceve la lunghezza del nome del database. Se *len* è NULL, la lunghezza del nome del database non viene restituita.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Puntatore DBCHAR alla stringa con terminazione Null per la parte del nome del database della stored procedure remota corrente. Se non è presente alcuna stored procedure remota corrente, viene restituito NULL e il parametro *len* viene impostato su -1.  
  
## <a name="remarks"></a>Remarks  
 Questa funzione restituisce solo il componente del database del nome dell'oggetto stored procedure remota. Non include gli identificatori facoltativi per il proprietario, il nome della stored procedure remota e il numero della stored procedure remota.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
