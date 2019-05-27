---
title: il carattere 0xFFFF non è valido come identificatore di oggetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35c7c65bc312cd20c057b5e2603e7a8f77ce8c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096911"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>Il carattere 0xFFFF non è valido come identificatore di oggetto
  È stato rilevato un identificatore di oggetto contenente il carattere 0xFFFF. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive non è possibile rinominare o fare riferimento a oggetti quali database, tabelle e colonne con identificatori contenenti tale carattere nella modalità di compatibilità del database 90 o successiva. Quando si esegue l'aggiornamento a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la modalità di compatibilità dei database utente non cambia. Prima di impostare la modalità di compatibilità del database 90 o successiva, rinominare l'oggetto che contiene il carattere 0xFFFF.  
  
 Per ulteriori informazioni sugli identificatori, vedere "Identificatori" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sulle modalità compatibilità del database, vedere "sp_dbcmptlevel" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
