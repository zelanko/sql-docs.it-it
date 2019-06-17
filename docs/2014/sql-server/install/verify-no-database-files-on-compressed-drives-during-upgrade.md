---
title: Verificare che siano presenti file di database su unità compresse durante il processo di aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41c183c72188cccb21838e1e574992bfb723c022
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091156"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>Verificare che durante il processo di aggiornamento non siano presenti file di database su unità compresse
  Sono presenti file di database in un'unità compressa. Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è possibile creare o aggiornare database in unità compresse.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare un'unità non compressa per i database di sistema e verificare che questi vengano aggiornati su unità non compresse. Tenere tuttavia presente che, dopo l'aggiornamento del database, è possibile copiare database e filegroup secondari di sola lettura in un file system compresso NTFS.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
