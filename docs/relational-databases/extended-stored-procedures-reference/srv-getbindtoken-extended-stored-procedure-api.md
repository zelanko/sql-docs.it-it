---
title: srv_getbindtoken (API delle stored procedure estese) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c4c413a3a84aa7db12ac4ecde7d41e3efd34525
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064103"
---
# <a name="srv_getbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (API delle stored procedure estese)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Ottiene un token di associazione della transazione nella sessione client corrente che richiama la stored procedure estesa.  
  
 La stored procedure estesa può quindi usare **sp_bindsession** per associare qualsiasi nuova sessione creata sullo stesso server alla transazione esistente in modo che la nuova sessione possa condividere lo stesso spazio di blocco della transazione con la sessione client che ha richiamato la stored procedure estesa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene tutte le informazioni utilizzate dalla libreria dell'API della stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *bindtoken*  
 Puntatore a un buffer in cui verrà copiato il token di associazione. Il token di associazione viene rappresentato come stringa con terminazioni Null. Il buffer specificato deve essere lungo almeno 255 byte.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Remarks  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>Per associare una sessione della stored procedure estesa alla sessione client che l'ha chiamata perché condividano lo stesso spazio di blocco della transazione  
  
1.  La stored procedure estesa chiama **svr_getbindtoken** per ottenere il token di associazione per la transazione corrente nella sessione. Il token viene restituito nel parametro *bindtoken* specificato.  
  
2.  La stored procedure estesa apre nuove sessioni sullo stesso server. Nella sessione la stored procedure estesa usa il token di associazione con **sp_bindsession** per associare la nuova sessione alla stessa transazione. La stored procedure estesa può creare più sessioni e può associare tutte le sessioni alla stessa transazione.  
  
3.  L'associazione di una sessione viene annullata quando viene restituita la stored procedure esterna o quando **sp_bindsession** viene chiamata con una stringa vuota.  
  
    > [!NOTE]  
    >  A una connessione condivisa può accedere solo una sessione associata per volta. Se una sessione esegue un'istruzione nel server o è in attesa di risultati dal server, nessun'altra sessione che condivide la stessa connessione associata può accedere al server fino a quando la sessione corrente non completa l'esecuzione dell'istruzione corrente. Se una sessione tenta di accedere alla connessione mentre il server è occupato, nella sessione in conflitto viene restituito un errore che indica che la connessione è in uso e che la sessione dovrà eseguire un nuovo tentativo in seguito.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
