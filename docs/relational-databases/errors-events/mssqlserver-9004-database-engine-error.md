---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fe4aa3b74af774543c5125652d8f860c68fb04fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118329"
---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9004|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LOG_CORRUPT|  
|Testo del messaggio|Si è verificato un errore durante l'elaborazione del log del database '%.*ls'.  Se possibile, ripristinarlo da un backup. Se non è disponibile un backup, potrebbe essere necessario ricompilare il log.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore nell'elaborazione del log durante un'operazione di rollback, recupero o replica. Potrebbe trattarsi di un errore rilevato dal sistema operativo o di un errore di consistenza interno rilevato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Azione dell'utente  
Per correggere l'errore, eseguire una delle operazioni seguenti:  
  
-   Eseguire il ripristino da un backup.  
  
-   Ricompilare il log.  
  
Esaminare inoltre il registro eventi e il log degli errori di sistema per individuare le cause all'interno del sistema che possono aver generato il problema.  
  
