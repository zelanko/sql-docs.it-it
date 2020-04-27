---
title: Regole di confronto e tipi di dati di integrazione CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 40c4abad803424ac9b274045f699785b85689644
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874849"
---
# <a name="collation-and-clr-integration-data-types"></a>Regole di confronto e tipi di dati di integrazione CLR
  In [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] l'oggetto `CompareInfo` gestisce le regole di confronto. Le API di stringa di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzano la proprietà `CompareInfo` associata all'oggetto `CultureInfo` del thread corrente per eseguire confronti tra stringhe. L'impostazione `CultureInfo` predefinita dell'oggetto è basata sulle impostazioni locali [!INCLUDE[msCoName](../../includes/msconame-md.md)] di Windows per il computer in cui [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione. Questo determina la semantica del confronto predefinita, se non viene specificata alcuna `CultureInfo` esplicita, per confronti di valori `System.String`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non modifica in modo esplicito la proprietà `CompareInfo` sulle regole di confronto del database o del server. Se richiesto, gli utenti devono impostare la proprietà `CompareInfo` appropriata nelle routine.  
  
## <a name="parameter-collation"></a>Regole di confronto dei parametri  
 Quando si crea una routine CLR (Common Language Runtime) e un parametro di un metodo CLR associato alla routine è di tipo `SQLString`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un'istanza del parametro con le regole di confronto predefinite del database che contiene la routine chiamante. Se un parametro non è del tipo `SqlType` (ad esempio, `String` anziché `SQLString`), le informazioni sulle regole di confronto provenienti dal database non vengono associate al parametro.  
  
## <a name="see-also"></a>Vedi anche  
 [Tipi di dati di SQL Server in .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
