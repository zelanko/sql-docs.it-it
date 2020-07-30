---
title: srv_rpcname (API Stored procedure estesa) | Microsoft Docs
description: Informazioni sul modo in cui srv_rpcname nell'API della stored procedure estesa restituisce il componente del nome della procedura per la stored procedure remota corrente.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcname
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
ms.openlocfilehash: 99e901a9ae1a14644d522b23747f1d242f8c95d3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248289"
---
# <a name="srv_rpcname-extended-stored-procedure-api"></a>srv_rpcname (API Stored procedure estesa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce il componente del nome della procedura per la stored procedure remota corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. In questo caso, l'handle che ha ricevuto la stored procedure remota. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *Len*  
 Puntatore a una variabile di tipo integer che riceve la lunghezza del nome del database. Se *len* è NULL, la lunghezza del nome della stored procedure remota non viene restituita.  
  
## <a name="returns"></a>Restituisce  
 Puntatore DBCHAR alla stringa con terminazione Null per il componente del nome della stored procedure remota della stored procedure remota corrente. Se non è presente alcuna stored procedure remota corrente, viene restituito NULL e *len* viene impostato su -1.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione restituisce solo il nome della stored procedure remota. Non include gli identificatori facoltativi per il proprietario, il nome del database e il numero della stored procedure remota.  
  
 Poiché è possibile chiamare **srv_rpcname** in assenza di stored procedure remote (non viene visualizzato alcun errore informativo), questa funzione offre un metodo per la verifica dell'eventuale presenza di una stored procedure remota.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
