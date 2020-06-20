---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 662d342064e8094400a6b672e21704877b4d0448
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033458"
---
# <a name="mssqlserver_3452"></a>MSSQLSERVER_3452
    
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
  
  
