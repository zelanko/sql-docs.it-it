---
title: srv_pfieldex (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_pfieldex
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f375f8befe51455679fdcb68fd4a79c05276fc8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050615"
---
# <a name="srv_pfieldex-extended-stored-procedure-api"></a>srv_pfieldex (API delle stored procedure estese)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce un puntatore ai dati che contengono il campo SRV_PROC richiesto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *campo*  
 Specifica il campo *srvproc* da restituire.  
  
|Campo|Descrizione|Tipo restituito|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|LCDI di messaggio della sessione corrente.|ULONG*|  
|SRV_INSTANCENAME|Nome dell'istanza (se si tratta di un'istanza denominata); in caso contrario, restituisce NULL.|WCHAR*|  
  
 *Len*  
 Puntatore a una variabile **int** che contiene la lunghezza in byte del valore *field* restituito. Se *len* è NULL, la lunghezza non viene restituita. Quando viene restituito NULL, **len* è impostato su 0.  
  
## <a name="returns"></a>Restituisce  
 Un puntatore ai dati il cui tipo dipende da *field*. Viene restituito NULL se *len* è NULL o *srvproc* è NULL. Se *field* non è noto, viene restituito NULL. Quando viene restituito NULL, **len* è impostato su 0.  
  
> [!IMPORTANT]  
>  Il buffer restituito dal server deve essere di sola lettura. In caso contrario, lo stato del server può risultare danneggiato.  
  
## <a name="remarks"></a>Osservazioni  
 **Nota sulla sicurezza** È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
