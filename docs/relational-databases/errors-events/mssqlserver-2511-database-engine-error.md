---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c28be4ae43225cc4593291285c09115829be8da2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780448"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
