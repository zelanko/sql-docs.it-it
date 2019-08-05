---
title: srv_setcoldata (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcoldata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcoldata
ms.assetid: 2e19205a-25ca-4d4a-916b-d591cf2c892b
author: rothja
ms.author: jroth
ms.openlocfilehash: 36020fb9df7b98338cd64a8e476b8da0b5196c0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119652"
---
# <a name="srv_setcoldata-extended-stored-procedure-api"></a>srv_setcoldata (API Stored procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Specifica l'indirizzo corrente per i dati di una colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_setcoldata (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
void *  
data   
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *column*  
 Indica il numero della colonna per il quale viene specificato l'indirizzo. Le colonne sono numerate a partire da 1.  
  
 *data*  
 Indicatore di misura per i dati di una colonna. La memoria allocata per *data* non deve essere liberata fino a quando i dati della colonna non vengono sostituiti da un'altra chiamata a **srv_setcoldata** o fino alla chiamata a **srv_senddone**.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Remarks  
 Ogni colonna della riga deve essere definita prima con **srv_describe**. Gli indirizzi dei dati della colonna sono impostati inizialmente con **srv_describe**. Se l'indirizzo dei dati della colonna cambia, è necessario chiamare **srv_setcoldata** per specificare il nuovo indirizzo dei dati e quindi **srv_setcoldata** separatamente per ogni colonna modificata.  
  
 I dati Null vengono rappresentati impostando la lunghezza della colonna su 0 con **srv_setcollen**. L'indirizzo dei dati viene quindi ignorato.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_describe &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
