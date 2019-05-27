---
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 54c1e71e8df3369cf6b3b92a0b0f39833e677a08
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945822"
---
# <a name="replication-functions---publishingservername"></a>Funzioni di replica - PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il nome del server di pubblicazione di origine per un database pubblicato che partecipa a una sessione di mirroring del database. Questa funzione viene eseguita in un'istanza del server di pubblicazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database di pubblicazione. Utilizzarla per determinare il server di pubblicazione originale del database pubblicato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 La funzione PUBLISHINGSERVERNAME viene utilizzata in tutti i tipi di replica.  
  
 La funzione PUBLISHINGSERVERNAME viene utilizzata quando nel database di pubblicazione esiste una sessione di mirroring del database tra il server di pubblicazione e un'istanza del partner per il mirroring.  
  
 Questa funzione deve essere eseguita nel contesto di un database di pubblicazione. Quando PUBLISHINGSERVERNAME viene eseguita in un database di pubblicazione nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server mirror, viene restituito il nome dell'istanza del server di pubblicazione dal quale ha origine il database pubblicato. Quando la funzione viene eseguita in un database nell'istanza del server mirror non pubblicato o pubblicato dall'istanza del server mirror dopo un failover, viene restituito il nome dell'istanza del server mirror. Quando questa funzione viene eseguita nell'istanza del server di pubblicazione originale, viene restituito il nome del server di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring e replica del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Funzioni di replica &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  
