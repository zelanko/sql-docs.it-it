---
title: Rimuovere i due punti seguenti parola chiave riservata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fc6882439338509a3c716129d9504f209ab1e555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065198"
---
# <a name="remove-colon-following-reserved-keyword"></a>Rimuovere i due punti (:) dopo le parole chiave riservate
  È stato rilevato uno script che contiene una parola chiave riservata seguita da due punti (:). Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale sintassi viene ignorata e le istruzioni vengono eseguite correttamente. Ora tale sintassi impedisce l'esecuzione dell'istruzione in modalità di compatibilità del database 100 o successiva.  
  
 La modalità di compatibilità dei database utente non cambia.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di impostare la modalità di compatibilità del database su 100 o successiva, modificare gli script rimuovendo i due punti (:) dopo le parole chiave riservate. Per ulteriori informazioni, vedere "sp_dbcmptlevel" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
