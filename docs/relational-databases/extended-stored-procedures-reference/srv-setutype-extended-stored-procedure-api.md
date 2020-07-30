---
title: srv_setutype (API Stored procedure estesa) | Microsoft Docs
description: Informazioni sulle srv_setutype. srv_setutype imposta il tipo di dati definito dall'utente per una colonna in una riga.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setutype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ecdbaef663059146f3ca6bd4a88305e12d4f495
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248193"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype (API Stored procedure estesa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
 *column*  
 Indica quale colonna impostare. Le colonne sono numerate a partire da 1.  
  
 *user_type*  
 Specifica il codice del tipo di dati definito dall'utente.  
  
## <a name="returns"></a>Restituisce  
 SUCCEED o FAIL. Restituisce FAIL se la colonna non esiste.  
  
## <a name="remarks"></a>Commenti  
 In una colonna sono presenti due tipi di dati: il tipo di dati effettivo e il tipo di dati definito dall'utente. Il tipo di dati definito dall'utente viene utilizzato da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare il tipo di dati effettivo definito dall'utente, se presente, e le informazioni sulla descrizione della colonna, ad esempio il supporto di valori null e aggiornabilità, per la colonna.  
  
 La funzione **srv_setutype** può essere chiamata in qualsiasi momento in cui *column* è stato definito con **srv_describe** e prima che sia stata inviata l'ultima riga.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_describe &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
