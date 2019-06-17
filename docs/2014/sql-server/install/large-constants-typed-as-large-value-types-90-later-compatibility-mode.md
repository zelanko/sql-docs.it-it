---
title: Costanti di grandi dimensioni vengono tipizzate come tipi di valori di grandi dimensioni in modalità di compatibilità 90 o versioni successive | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c7aded5577e28d94f42e108e46bb8a9c3cd6020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094084"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>In modalità di compatibilità 90 o successiva per le costanti di grandi dimensioni vengono utilizzati i tipi di dati per valori di grandi dimensioni
  È stata rilevata la presenza di costanti di grandi dimensioni. Le costanti stringa di caratteri e le costanti binarie di dimensioni maggiori di 8.000 byte vengono considerate come tipi di dati di oggetti di grandi dimensioni in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive le costanti carattere, Unicode e binarie di grandi dimensioni vengono tipizzate come tipi di valori di grandi dimensioni.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Quando si utilizzano funzioni stringa, ad esempio CHARINDEX e PATINDEX, con costanti stringa di dimensioni maggiori di 8.000 byte, [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] restituisce il numero di errore 8116 e [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive restituiscono il numero di errore 8152.  
  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] le funzioni stringa restituiscono l'errore 8116 quando vengono utilizzate con i tipi di dati `text`, `ntext` e `image`.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive, le costanti di grandi dimensioni vengono considerate rispettivamente come tipi di dati `varchar(max)`, `nvarchar(max)` e `varbinary(max)`. Questi tipi di dati sono compatibili con le funzioni stringa.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive le funzioni stringhe, ad esempio CHARINDEX e PATINDEX, presuppongono che la stringa contenente la sequenza di caratteri da trovare sia minore di 8.000 byte. Per questo motivo, per CHARINDEX e PATINDEX viene generato l'errore 8152.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
