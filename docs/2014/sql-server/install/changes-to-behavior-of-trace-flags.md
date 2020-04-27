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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66096608"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Modifiche al comportamento dei flag di traccia
  I flag di traccia globali impostati da una sessione diventano immediatamente effettivi nelle altre sessioni. Alcuni flag di traccia di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] non esistono in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Si consiglia di disabilitare tutti i flag di traccia prima di eseguire l'aggiornamento. I flag di traccia che modificano la disponibilità o le modalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] recupero del database potrebbero impedire al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di di aggiornare correttamente l'istanza di. È possibile attivare i flag di traccia dopo avere verificato che sono necessari e sono ancora validi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se è necessario riabilitare i flag di traccia, eseguire test aggiuntivi sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta flag di traccia a livello di sessione e globale. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] i flag di traccia possono essere specificati come locali o globali utilizzando un argomento aggiuntivo (-1) nel comando DBCC TRACEON. Se questo argomento non viene specificato, il valore predefinito è locale.  
  
 Inoltre, in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], un flag di traccia impostato nella sessione a non diventa automaticamente effettivo in una sessione B già esistente. Questo flag di traccia viene invece applicato solo dopo la prima volta che un flag di traccia viene impostato nella sessione B. Questo comportamento è non deterministico [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] in e è deterministico in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, in cui i flag di traccia globali impostati nella sessione a vengono impostati immediatamente in altre sessioni simultanee.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
