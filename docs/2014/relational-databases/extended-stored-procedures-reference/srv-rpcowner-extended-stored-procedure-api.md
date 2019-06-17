---
title: srv_rpcowner (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcowner
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 68e5d0214a2bd14a466b7a0c40f792031d3fac5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745502"
---
# <a name="srvrpcowner-extended-stored-procedure-api"></a>srv_rpcowner (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce il componente proprietario per la stored procedure remota corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBCHAR * srv_rpcowner (  
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
  
 *len*  
 Puntatore a una variabile di tipo integer che riceve la lunghezza del nome del proprietario. Il parametro *len* può essere NULL. In tal caso, non viene restituita la lunghezza del componente proprietario.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Puntatore DBCHAR al componente proprietario con terminazione Null per la stored procedure remota corrente. Se non è presente alcuna stored procedure remota corrente, viene restituito NULL e *len* viene impostato su -1.  
  
## <a name="remarks"></a>Note  
 Questa funzione restituisce solo il componente proprietario della stored procedure remota. Non include gli identificatori facoltativi per il nome, il nome della stored procedure remota e il numero della stored procedure remota.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
  
