---
description: MSSQLSERVER_41365
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e370cafb16d5eceb2caed96b561862ea93b68205
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460925"
---
# <a name="mssqlserver_41365"></a>MSSQLSERVER_41365
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41365|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HK_MERGE_SCHEDULE_ERROR|  
|Testo del messaggio|La richiesta di unione per l'intervallo della transazioni [%ld, %ld) sul database %.*ls non è stata pianificata. I file del checkpoint che rappresentano l'intervallo non sono disponibili per unione o parte di un'unione in corso.|  
  
## <a name="explanation"></a>Spiegazione  
I file del checkpoint che rappresentano l'intervallo non sono disponibili per unione o parte di un'unione in corso.  
  
## <a name="user-action"></a>Azione dell'utente  
Fornire un migliore intervallo di transazioni per merge/attesa prima di eseguire la stessa richiesta. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
[OLTP in memoria &#40;ottimizzazione per la memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
