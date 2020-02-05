---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6bf076dd8a3dc3dc912ec7ec2155e477dff83f30
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67912138"
---
# <a name="mssqlserver_12304"></a>MSSQLSERVER_12304
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|12304|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|Testo del messaggio|L'utilizzo di un tipo di tabella con ottimizzazione per la memoria in cui viene utilizzata la proprietà IDENTITY con una delle relative colonne non è supportato quando si utilizza il tipo al di fuori del contesto di una stored procedure compilata in modo nativo.|  
  
## <a name="user-action"></a>Azione dell'utente  
Non utilizzare un tipo di tabella ottimizzata per la memoria in cui viene utilizzata la proprietà Identity con una delle relative colonne.  
  
## <a name="see-also"></a>Vedere anche  
[OLTP in memoria &#40;ottimizzazione per la memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
