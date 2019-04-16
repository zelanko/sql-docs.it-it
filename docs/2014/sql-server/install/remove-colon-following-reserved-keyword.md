---
title: Parola chiave riservata segue i due punti Remove | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f68a641caf21e6cc1dfdefbcb31ff78a1fd8aa6
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583034"
---
# <a name="remove-colon-following-reserved-keyword"></a>Rimuovere i due punti (:) dopo le parole chiave riservate
  È stato rilevato uno script che contiene una parola chiave riservata seguita da due punti (:). Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale sintassi viene ignorata e le istruzioni vengono eseguite correttamente. Ora tale sintassi impedisce l'esecuzione dell'istruzione in modalità di compatibilità del database 100 o successiva.  
  
 La modalità di compatibilità dei database utente non cambia.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di impostare la modalità di compatibilità del database su 100 o successiva, modificare gli script rimuovendo i due punti (:) dopo le parole chiave riservate. Per ulteriori informazioni, vedere "sp_dbcmptlevel" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
