---
title: Aggiornare tutti i server di destinazione prima di aggiornare il server master | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b6e08a384e20d64a7002171059db0d35dfd94a7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091469"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>Aggiornare tutti i server di destinazione prima di aggiornare il server master
  Prima di aggiornare il server master, aggiornare tutti i computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che sono configurati come server di destinazione.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Descrizione  
 Per automatizzare l'amministrazione negli ambienti multiserver, è necessario disporre almeno di un server master e di un server di destinazione. Il server master distribuisce processi ai server di destinazione e riceve eventi da tali server. Nel server master è inoltre archiviata la copia centrale delle definizioni di processo per i processi eseguiti nei server di destinazione.  
  
 Se il server corrente è configurato come server master, prima di aggiornare il server master aggiornare tutti i server di destinazione.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Se non è possibile aggiornare tutti i server di destinazione prima di aggiornare il server master, è necessario escludere tutti i server di destinazione e reintegrarli dopo l'aggiornamento.  
  
 Per altre informazioni, vedere gli argomenti "Automatizzazione amministrazione in un'organizzazione," "procedura: Escludere un Server di destinazione da un Server Master,"e" procedura: Integrare un Server di destinazione in un Master"nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
