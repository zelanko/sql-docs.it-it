---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b30cd4786e278b4fa88eb4264165e0c1449eeeb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985952"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3452|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|REC_CHECKIDENTITY|  
|Testo del messaggio|Durante il recupero del database '%.*ls' (%d) è stata rilevata una possibile inconsistenza dei valori Identity nella tabella con ID %d. Eseguire DBCC CHECKIDENT ('%.\*ls').|  
  
## <a name="explanation"></a>Spiegazione  
Durante l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nel processo di recupero dei valori Identity nel database è stata rilevata un'incoerenza tra i metadati.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire DBCC CHECKIDENT.  
  
