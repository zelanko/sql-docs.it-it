---
title: Supporto UTF-16 in SQL Server Native Client 11,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b28d869a6e33969550751158e321ec24062bf6ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707152"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Supporto per UTF-16 in SQL Server Native Client 11.0
  A partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , se si fornisce un buffer a lunghezza fissa quando si associa un risultato della colonna o un parametro di output e se il `wchar` carattere scritto nel buffer prima del carattere di terminazione è un punto di codice surrogato alto di una coppia di surrogati e se il `wchar` carattere successivo è un punto di codice surrogato basso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client non aggiungerà il punto di codice surrogato alto al buffer  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
