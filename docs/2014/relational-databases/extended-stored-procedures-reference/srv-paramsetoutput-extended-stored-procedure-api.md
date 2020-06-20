---
title: srv_paramsetoutput (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramsetoutput
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
ms.openlocfilehash: c1bfdd083973dd5dc3a27b9087ca912812815bca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050649"
---
# <a name="srv_paramsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Imposta il valore di un parametro restituito. Questa funzione sostituisce la funzione **srv_paramset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Handle per una connessione client.  
  
 *n*  
 Numero ordinale del parametro da impostare. Il primo parametro è 1.  
  
 *pbData*  
 Puntatore al valore dei dati da inviare di nuovo al client come parametro restituito della stored procedure.  
  
 *cbLen*  
 Lunghezza effettiva dei dati da restituire. Se il tipo di dati del parametro specifica i valori di una lunghezza costante e non consente valori Null (ad esempio, *srvbit* or *srvint1*), *cbLen* viene ignorato. Il valore 0 significa dati di lunghezza zero se *fNull* è FALSE.  
  
 *fNull*  
 Flag che indica se il valore del parametro restituito è NULL. Impostare questo flag su TRUE se il parametro deve essere impostato su NULL. Il valore predefinito è FALSE. Se *fNull* è impostato su TRUE, *cbLen* deve essere impostato su 0; in caso contrario la funzione avrà esito negativo.  
  
## <a name="returns"></a>Restituisce  
 Se le informazioni sul parametro sono state impostate correttamente, viene restituito SUCCEED; in caso contrario, FAIL. FAIL viene restituito nei seguenti casi:  
  
-   Il parametro non è un parametro restituito.  
  
-   L'argomento *cbLen* non è valido.  
  
## <a name="remarks"></a>Osservazioni  
 **Nota sulla sicurezza** È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
