---
title: Supporto per UTF-16 in SQL Server Native Client 11.0 | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205118"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Supporto per UTF-16 in SQL Server Native Client 11.0
  A partire [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], se si fornisce un buffer a lunghezza fissa quando si associa un parametro di output o risultato di colonna e se il `wchar` carattere scritto nel buffer prima che il carattere di terminazione è un punto di codice surrogato alto di una coppia di surrogati e se la prossima `wchar` carattere è un punto di codice surrogato basso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non aggiungerà il punto di codice surrogato alto nel buffer.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
