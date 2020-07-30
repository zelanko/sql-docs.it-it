---
title: srv_rpcoptions (API Stored procedure estesa) | Microsoft Docs
description: Informazioni sul modo in cui srv_rpcoptions nell'API della stored procedure estesa restituisce le opzioni di runtime per il stored procedure remoto corrente.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcoptions
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d4bd331b54b4bb555fcc6cdbe59155a553332eb
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332470"
---
# <a name="srv_rpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions (API delle stored procedure estese)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Restituisce le opzioni di runtime per la stored procedure remota corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. In questo caso, l'handle che ha ricevuto la stored procedure remota. La struttura contiene informazioni utilizzate dalla libreria dell'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
## <a name="returns"></a>Restituisce  
 Una bitmap che contiene i flag di esecuzione uniti in un'operazione con OR logico per la stored procedure remota corrente. Se non è presente alcuna stored procedure remota corrente, viene restituito 0 e viene generato un messaggio.  
  
## <a name="remarks"></a>Osservazioni  
 Nella tabella seguente viene descritto ciascun flag di esecuzione.  
  
|Flag di esecuzione|Descrizione|  
|--------------------|-----------------|  
|SRV_NOMETADATA|Il client ha richiesto risultati senza informazioni sui metadati. Questo flag viene utilizzato solo quando il client comunica con un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un'applicazione API delle stored procedure estese non può omettere le informazioni sui metadati.|  
|SRV_RECOMPILE|Il client ha richiesto di ricompilare la stored procedure remota prima di eseguirla. Questo flag non può essere applicato a un'applicazione API delle stored procedure estese.|  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
