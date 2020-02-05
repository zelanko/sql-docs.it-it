---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 39d3edc1b85dba6c223cc4b4e5b3d3250b48d489
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132285"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8649|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|COST_TOO_HIGH|  
|Testo del messaggio|La query è stata annullata perché il suo costo stimato (%d) è maggiore della soglia configurata, pari a %d. Contattare l'amministratore del sistema.|  
  
## <a name="explanation"></a>Spiegazione  
La query è stata annullata perché il suo costo stimato supera la soglia configurata impostata per QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Azione dell'utente  
Impostare l'opzione QUERY_GOVERNOR_COST_LIMIT su un valore più elevato.  
  
## <a name="see-also"></a>Vedere anche  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
