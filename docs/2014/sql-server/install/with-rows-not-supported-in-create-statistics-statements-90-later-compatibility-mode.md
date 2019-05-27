---
title: WITH ROWS non è supportata nelle istruzioni CREATE STATISTICS in modalità di compatibilità 90 o successiva | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090964"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>Quando è attiva la modalità di compatibilità 90 o successiva la clausola WITH ROWS non è supportata nelle istruzioni CREATE STATISTICS
  Se si esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con modalità di compatibilità 90 o successiva, l'utilizzo di WITH ROWS nelle istruzioni CREATE STATISTICS non è supportato.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le istruzioni CREATE STATISTICS che includono WITH ROWS specificando WITH SAMPLE *numero* righe, oppure specificando altre opzioni conformi alla sintassi documentata. Per ulteriori informazioni, vedere l'argomento "CREATE STATISTICS (Transact-SQL) nella documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
