---
title: Specificare la parola chiave WITH quando si usano gli hint di tabella in modalità di compatibilità 90 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: de4abebf061d2eaa419d8b71c9cf5a50d3e505db
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582944"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>Specificare la parola chiave WITH quando si utilizzano hint di tabella in modalità di compatibilità 90
  Gli hint di tabella sono supportati nella clausola FROM di una query solo se vengono specificati utilizzando la parola chiave WITH, con alcune eccezioni. Per ulteriori informazioni, vedere gli argomenti "FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])" e "Hint di tabella ([!INCLUDE[tsql](../../includes/tsql-md.md)])" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le query che includono hint di tabella nella clausola FROM includendo la parola chiave WITH prima degli hint di tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
