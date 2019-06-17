---
title: srv_alloc (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_alloc
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8677bb878094bf2345f00b7c6838a43b653faac6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62939638"
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc (API delle stored procedure estese)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Alloca memoria dinamicamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *size*  
 Specifica il numero di byte da allocare.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Un puntatore al nuovo spazio allocato. Se i byte di *size* non possono essere allocati, viene restituito un puntatore Null.  
  
## <a name="remarks"></a>Remarks  
 La funzione **srv_alloc** è equivalente alla funzione **GlobalAlloc** dell'API [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Normali funzioni di gestione della memoria di runtime del linguaggio C dell'API Windows possono essere utilizzate in un'applicazione API di stored procedure estese.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
  
