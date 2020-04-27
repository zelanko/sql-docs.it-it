---
title: Posizione del recupero successivo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c47f1a8692cf7d2e3fb4f00c64770b3b0c69e5a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63183635"
---
# <a name="next-fetch-position"></a>Posizione del recupero successivo
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client tiene traccia della successiva posizione di recupero, in modo che una sequenza di chiamate al metodo **GetNextRows** (senza salti, modifiche di direzione o chiamate intermedie ai metodi **FindNextRow**, **Seek**o **RestartPosition** ) Legga l'intero set di righe senza ignorare o ripetere alcuna riga. La posizione del recupero successiva viene modificata chiamando **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek** oppure chiamando **FindNextRow** con un valore *pBookmark* Null. La chiamata a **FindNextRow** con un valore *pBookmark* non Null non influisce sulla posizione del recupero successivo.  
  
## <a name="see-also"></a>Vedi anche  
 [Recupero di righe](fetching-rows.md)  
  
  
