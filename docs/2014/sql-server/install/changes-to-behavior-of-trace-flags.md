---
title: Modifiche al comportamento dei flag di traccia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 447e6d4d35fa77f71f1a7a1b90a5a782e0ccebcc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096608"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Modifiche al comportamento dei flag di traccia
  I flag di traccia globali impostati da una sessione diventano immediatamente effettivi nelle altre sessioni. Alcuni flag di traccia di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] non esistono in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Si consiglia di disabilitare tutti i flag di traccia prima di eseguire l'aggiornamento. I flag di traccia che modificano le modalità di disponibilità o il ripristino di database potrebbero impedire il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] da aggiornare correttamente l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile attivare i flag di traccia dopo avere verificato che sono necessari e sono ancora validi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se è necessario riabilitare i flag di traccia, eseguire test aggiuntivi sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta flag di traccia a livello di sessione e globale. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] i flag di traccia possono essere specificati come locali o globali utilizzando un argomento aggiuntivo (-1) nel comando DBCC TRACEON. Se questo argomento non viene specificato, il valore predefinito è locale.  
  
 Inoltre, in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], un flag di traccia impostato nella sessione A non diventa automaticamente effettivo in una sessione b già esistente Al contrario, questo flag di traccia ha effetto solo dopo la prima volta che un flag di traccia viene impostato nella sessione B. Questo comportamento è non deterministico in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ed è deterministico in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, in cui flag di traccia globali impostati nella sessione A vengono immediatamente impostati in altre sessioni simultanee.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
