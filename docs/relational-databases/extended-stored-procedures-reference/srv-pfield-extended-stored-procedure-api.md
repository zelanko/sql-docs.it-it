---
title: srv_pfield (API Stored procedure estesa) | Microsoft Docs
description: Informazioni sul modo in cui srv_pfield nell'API della stored procedure estesa restituisce informazioni su una connessione al database.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
author: rothja
ms.author: jroth
ms.openlocfilehash: 12d985ca974f923f37db9d19de048e14af143271
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248313"
---
# <a name="srv_pfield-extended-stored-procedure-api"></a>srv_pfield (API della stored procedure estesa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce informazioni su una connessione a un database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore che identifica una connessione al database.  
  
 *campo*  
 Specifica i dati nella connessione da restituire.  
  
|Valore|Restituisce|  
|-----------|-------------|  
|SRV_APPLNAME|Nome dell'applicazione fornito dal client quando ha stabilito la connessione.|  
|SRV_BCPFLAG|Flag impostato su TRUE se il client si prepara per un'operazione di copia bulk; in caso contrario, è impostato su FALSE.|  
|SRV_CLIB|Nome della libreria che consente al client di comunicare con un server.|  
|SRV_CPID|ID del processo client nel computer di origine client.|  
|SRV_HOST|Nome del computer del client fornito dal client quando ha stabilito la connessione.|  
|SRV_LIBVERS|Versione della libreria client.|  
|SRV_LSECURE|Flag. TRUE se la connessione utilizza sicurezza integrata per l'accesso.|  
|SRV_NETWORK_MODULE|Nome della DLL di rete utilizzata dalla connessione.|  
|SRV_NETWORK_VERSION|Versione della DLL di rete utilizzata dalla connessione.|  
|SRV_NETWORK_CONNECTION|Stringa di connessione passata alla DLL di rete usata per la connessione *srvproc* corrente.|  
|SRV_PIPEHANDLE|Stringa che contiene l'handle di pipe di un client connesso oppure valore NULL se il client è connesso in una rete che non utilizza named pipe. Per utilizzare questo handle come handle di pipe valido con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, convertire questa stringa in numero intero.|  
|SRV_RMTSERVER|Server dal quale ha eseguito l'accesso il processo del client. Se l'accesso è da un client, questo valore è una stringa vuota.|  
|SRV_ROWSENT|Numero di righe già inviate da *srvproc* per il set di risultati corrente.|  
|SRV_SPID|ID del thread di server di *srvproc*. Per le stored procedure estese, questo valore coincide con quello della colonna **kpid** di **sys.sysprocesses** e può cambiare nel tempo.|  
|SRV_SPROC_CODEPAGE|Tabella codici utilizzata dal server per interpretare dati multibyte.|  
|SRV_STATUS|Stato corrente di *srvproc*: in esecuzione o chiusa|  
|SRV_TYPE|Tipo di connessione di *srvproc*. Se viene restituito server, la connessione *srvproc* viene eseguita da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se viene restituito client, la connessione *srvproc* viene eseguita da DB-Library o da un client ODBC.|  
|SRV_USER|Nome utente della connessione.|  
|||  
  
 *Len*  
 Puntatore a una variabile **int** che contiene la lunghezza del valore *field* restituito. Se *len* è NULL, la lunghezza della stringa non viene restituita.  
  
## <a name="returns"></a>Restituisce  
 Un puntatore a una stringa con terminazione Null che contiene il valore corrente per il campo specificato nella struttura SRV_PROC. Se il campo è vuoto, viene restituito un puntatore valido a una stringa vuota e *len* contiene 0. Se il campo non è noto, viene restituito NULL e *len* contiene il valore -1.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e l'analisi della sicurezza, visitare il sito Web [Security Developer Center](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
