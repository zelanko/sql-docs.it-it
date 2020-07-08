---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a459a23e9f74f04baed73c24c25c1757fbcc047f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694131"
---
# <a name="mssqlserver_41333"></a>MSSQLSERVER_41333
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41333|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Testo del messaggio|Le seguenti transazioni devono accedere alle tabelle con ottimizzazione per la memoria e alle stored procedure compilate in modo nativo con isolamento dello snapshot: transazioni RepeatableRead, transazioni Serializable e transazioni che accedono alle tabelle senza ottimizzazione per la memoria in isolamento RepeatableRead o Serializable.|  
  
## <a name="explanation"></a>Spiegazione  
Sono presenti restrizioni relative all'uso di livelli di isolamento più elevati tra le transazioni basate su disco e le transazioni di XTP.  
  
## <a name="user-action"></a>Azione dell'utente  
Non tentare operazioni con un livello di isolamento alto nelle tabelle ottimizzate per la memoria (e procedure compilate in modo nativo) e nelle tabelle basate su disco.  
  
Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
[OLTP in memoria &#40;ottimizzazione per la memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
