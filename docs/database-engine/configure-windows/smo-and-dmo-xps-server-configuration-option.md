---
title: Opzioni di configurazione del server SMO e DMO XPs | Microsoft Docs
description: Informazioni su come abilitare le stored procedure estese SMO (SQL Server Management Object) in un server. Visualizzare informazioni sull'opzione di configurazione "SMO and DMO XPs".
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a636f58ba3f7e9e178489e87af4dc3aa777fdbab
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773614"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>Opzioni di configurazione del server SMO e DMO XPs
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'opzione SMO and DMO XPs consente di abilitare le stored procedure estese SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object) nel server.  
  
 Si noti che, a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], DMO è stato rimosso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I valori possibili sono illustrati nella tabella seguente:  
  
|valore|Significato|  
|-----------|-------------|  
|0|Le stored procedure estese SMO non sono disponibili.|  
|1|Le stored procedure estese SMO sono disponibili. Questa è la modalità predefinita.|  
  
 L'impostazione ha effetto immediato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono abilitate le stored procedure estese SMO.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida alla programmazione di SQL Server Management Objects &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
