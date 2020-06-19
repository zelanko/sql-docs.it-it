---
title: I database di sola lettura non possono essere aggiornati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ba48ed2bd80961a4949dc13f04fed0637ecc27ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054682"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>Non è possibile aggiornare database di sola lettura
  Alcuni database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non possono essere aggiornati.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 È stato rilevato un database di sola lettura. Per aggiornare il database, è necessario che sia accessibile in scrittura dal programma di installazione.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Quando nessuno utilizza il database, utilizzare l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzione di Enterprise Manager, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o alter database per modificare il database in lettura/scrittura. Per impostare il database in lettura/scrittura, utilizzare l'istruzione seguente.  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 Per ulteriori informazioni sull'istruzione ALTER DATABASE, vedere l'argomento "ALTER DATABASE ([!INCLUDE[tsql](../../includes/tsql-md.md)])" argomento nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
