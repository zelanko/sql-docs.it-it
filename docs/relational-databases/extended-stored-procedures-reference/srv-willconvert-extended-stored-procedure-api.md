---
title: srv_willconvert (Api Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e091dded3b9c763be6d5d891ac7026146feb0a0d
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246660"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (Api Stored Procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Determina se una conversione di un tipo di dati specifico è disponibile all'interno della Libreria ODS.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srctype*  
 Indica il tipo di dati da convertire. Questo parametro può appartenere a qualsiasi tipo di dati dell'API Stored procedure estesa.  
  
 *desttype*  
 Indica il tipo di dati nel quale devono essere convertiti i dati di origine. Questo parametro può appartenere a qualsiasi tipo di dati dell'API Stored procedure estesa.  
  
## <a name="returns"></a>Valori di codice restituiti  
 TRUE se la conversione del tipo di dati è supportata. In caso contrario, FALSE.  
  
## <a name="remarks"></a>Remarks  
 Per una descrizione di ogni tipo di dati, vedere [Tipi di dati &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://www.microsoft.com/en-us/msrc?rtc=1).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_convert &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
