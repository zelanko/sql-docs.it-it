---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12fc1ff12cd7c464a2de893b4c2c5f338063dce0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860783"
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|125|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Per le espressioni Case sono consentiti solo %d livelli di nidificazione.|  
  
## <a name="explanation"></a>Spiegazione  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente solo 10 livelli di nidificazione nelle espressioni CASE.  
  
## <a name="user-action"></a>Azione dell'utente  
Ridurre il livello di istruzioni CASE a un massimo di 10.  
  
## <a name="see-also"></a>Vedere anche  
[CASE &#40;Transact-SQL&#41;](~/t-sql/language-elements/case-transact-sql.md)  
  
