---
title: srv_willconvert (Api Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_willconvert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0af2ec4471dc24af0fdb02576adad312ed35069f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740701"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (Api Stored Procedure estesa)
    
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
  
## <a name="remarks"></a>Note  
 Per una descrizione di ogni tipo di dati, vedere [Tipi di dati &#40;API Stored procedure estesa&#41;](data-types-extended-stored-procedure-api.md).  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_convert &#40;API Stored procedure estesa&#41;](srv-convert-extended-stored-procedure-api.md)  
  
  
