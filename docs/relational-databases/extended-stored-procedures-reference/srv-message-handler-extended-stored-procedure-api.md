---
title: srv_message_handler (API Stored procedure estesa)
description: Informazioni su srv_message_handler e su come viene chiamato il gestore di messaggi dell'API stored procedure estesa installata.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_message_handler
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_message_handler
ms.assetid: 41bcd057-436f-4fa8-8293-fc8057a30877
author: rothja
ms.author: jroth
ms.openlocfilehash: 2edc96558c00b43dfe9d9b346ad75c32b42af1cd
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332357"
---
# <a name="srv_message_handler-extended-stored-procedure-api"></a>srv_message_handler (API Stored procedure estesa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Chiama il gestore dei messaggi dell'API Stored procedure estesa installato. Questa funzione viene in genere utilizzata per chiamare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un stored procedure esteso per registrare un errore (definito dalla stored procedure estesa) nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log degli errori o nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_message_handler (  
SRV_PROC *  
srvproc  
,  
int  
errornum  
,  
BYTE   
severity  
,  
BYTE  
state  
,  
int  
oserrnum  
,  
char *  
errtext  
,  
int  
errtextlen  
,  
char *  
oserrtext  
,  
int  
oserrtextlen  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. Il parametro *srvproc* contiene informazioni usate per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *errornum*  
 Numero dell'errore definito dalla stored procedure estesa. Questo numero deve essere compreso tra 50.001 e 2.147.483.647.  
  
 *severity*  
 Valore di gravità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standard per l'errore. Questo numero deve essere compreso tra 0 e 24.  
  
 *state*  
 Valore di stato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'errore.  
  
 *oserrnum*  
 Numero dell'errore del sistema operativo. Questo argomento viene ignorato.  
  
 *errtext*  
 Descrizione dell'errore della stored procedure estesa *errornum*.  
  
 *errtextlen*  
 Lunghezza della stringa dell'errore della stored procedure estesa *errtext*.  
  
 *oserrtext*  
 Descrizione dell'errore del sistema operativo *oserrnum*. Questo argomento viene ignorato.  
  
 *oserrtextlen*  
 Lunghezza della stringa dell'errore del sistema operativo *oserrtext*.  
  
## <a name="returns"></a>Restituisce  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Commenti  
 La funzione **srv_message_handler** consente a una stored procedure estesa di integrarsi con le funzioni centralizzate di registrazione e report errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli avvisi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere stabiliti per gli eventi dalle stored procedure estese e SQL Server Agent monitorerà queste condizioni di avviso.  
  
 Se il messaggio di errore è più lungo, viene troncato a 412 byte.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://msdn.microsoft.com/security/).  
  
  
