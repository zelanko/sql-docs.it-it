---
title: srv_setutype (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2439b19c4550d07b8d50a0bed6d72b603b1601a8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745790"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Imposta il tipo di dati definito dall'utente per una colonna di una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *colonna*  
 Indica quale colonna impostare. Le colonne sono numerate a partire da 1.  
  
 *user_type*  
 Specifica il codice del tipo di dati definito dall'utente.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL. Restituisce FAIL se la colonna non esiste.  
  
## <a name="remarks"></a>Osservazioni  
 In una colonna sono presenti due tipi di dati: il tipo di dati effettivo e il tipo di dati definito dall'utente. Il tipo di dati definito dall'utente viene utilizzato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da per archiviare il tipo di dati effettivo definito dall'utente, se presente, e le informazioni sulla descrizione della colonna, ad esempio il supporto di valori null e aggiornabilità, per la colonna.  
  
 La funzione **srv_setutype** può essere chiamata in qualsiasi momento in cui *column* è stato definito con **srv_describe** e prima che sia stata inviata l'ultima riga.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedi anche  
 [srv_describe &#40;API Stored procedure estesa&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
