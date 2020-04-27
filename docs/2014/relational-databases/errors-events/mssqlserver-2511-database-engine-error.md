---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1748e8b483eecee43da921bd268d419408924af3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62868965"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2511|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_KEYS_OUT_OF_ORDER|  
|Testo del messaggio|Errore di tabella: ID di oggetto %d, ID di indice %d, ID di partizione %I64d, ID di unità di allocazione %I64d (tipo %.*ls). Chiavi non ordinate alla pagina %S_PGID, slot %d e %d.|  
  
## <a name="explanation"></a>Spiegazione  
 Nell'indice specificato sono state rilevate chiavi non ordinate. La pagina in cui sono contenute le chiavi può essere danneggiata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Ricompilare l'indice specificato utilizzando l'istruzione ALTER INDEX REBUILD.  
  
  
