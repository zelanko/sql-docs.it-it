---
title: Rimuovere le istruzioni che modificano le autorizzazioni a livello di colonna per oggetti di sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b377ac0b9baacdab6461a0e62174538902939bd8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093025"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>Rimuovere le istruzioni che modificano le autorizzazioni a livello di colonna per gli oggetti di sistema
  Sono state rilevate autorizzazioni non standard a livello di colonna per alcuni oggetti di sistema. Tali modifiche alle autorizzazioni non verranno mantenute durante l'aggiornamento. Le autorizzazioni a livello di colonna per gli oggetti di sistema non sono inoltre più supportate. Rimuovere dalle applicazioni tutte le istruzioni che impostano autorizzazioni a livello di colonna per oggetti di sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere dalle applicazioni le istruzioni che concedono, negano o revocano autorizzazioni a livello di colonna per oggetti di sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
