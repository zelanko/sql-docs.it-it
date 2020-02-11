---
title: Regole di confronto e tipi di dati di integrazione CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 51345c498277cc7013bbc05784022f65d77aef65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081343"
---
# <a name="collation-and-clr-integration-data-types"></a>Regole di confronto e tipi di dati di integrazione CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]l'oggetto **CompareInfo** gestisce le regole di confronto. Le API di stringa di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzano la proprietà **CompareInfo** associata all'oggetto **CultureInfo** del thread corrente per eseguire confronti tra stringhe. L'impostazione predefinita dell'oggetto **CultureInfo** si basa sulle impostazioni locali di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows del computer sul quale [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione. Questo determina la semantica del confronto predefinita, se non viene specificata alcuna **CultureInfo** esplicita, per confronti di valori **System.String** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]non modifica in modo esplicito la proprietà **CompareInfo** per le regole di confronto del database o del server. Se richiesto, gli utenti devono impostare la proprietà **CompareInfo** appropriata nelle routine.  
  
## <a name="parameter-collation"></a>Regole di confronto dei parametri  
 Quando si crea una routine Common Language Runtime (CLR) e un parametro di un metodo CLR associato alla routine è di tipo **SqlString**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un'istanza del parametro con le regole di confronto predefinite del database che contiene la routine chiamante. Se un parametro non è del tipo **SqlType** (ad esempio, **String** anziché **SQLString**), le informazioni sulle regole di confronto provenienti dal database non vengono associate al parametro.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
