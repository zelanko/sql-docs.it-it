---
title: Supporto UTF-16 in SQL Server Native Client 11,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63205118"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Supporto per UTF-16 in SQL Server Native Client 11.0
  A partire [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]da, se si fornisce un buffer a lunghezza fissa quando si associa un risultato della colonna o un parametro `wchar` di output e se il carattere scritto nel buffer prima del carattere di terminazione è un punto di codice surrogato alto di una `wchar` coppia di surrogati e se il carattere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] successivo è un punto di codice surrogato basso, Native client non aggiungerà il punto di codice surrogato alto al buffer  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
