---
title: Modificare le applicazioni in modo da prevedere valori bigint da sysperfinfo. cntr_value | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ced1e07b5423dcdc7c13d24e8528a2b6ac240aaa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093951"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntr_value"></a>Modificare le applicazioni in modo da prevedere valori bigint da sysperfinfo.cntr_value
  sysperfinfo restituisce un `bigint` valore per la colonna cntr_value.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le applicazioni che utilizzano sysperfinfo per assicurarsi che siano in grado di gestire i valori `bigint` della colonna cntr_value.  
  
> [!NOTE]  
>  sysperfinfo è una vista di compatibilità. Utilizzare invece la vista a gestione dinamica sys. dm_os_performance_counter.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
