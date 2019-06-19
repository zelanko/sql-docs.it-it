---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1064b834d24c820da49a1791a6a319f27c27d301
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867988"
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|MSSQLSERVER|  
|ID evento|3937|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Testo del messaggio|Durante il rollback di una transazione, si è verificato un errore nel tentativo di notificare l'esecuzione del rollback di una transazione al driver del filtro FILESTREAM. Codice errore: 0x%0x.|  
  
## <a name="explanation"></a>Spiegazione  
 Durante l'invio di una notifica di esecuzione del rollback di una transazione, è stato restituito un errore dal driver RsFx, probabilmente a causa di risorse insufficienti. Questa situazione potrebbe provocare una piccola perdita di memoria nel driver del filtro RsFx, in cui tuttavia verrà liberato spazio quando il processo sqlservr.exe che creato la transazione termina.  
  
## <a name="user-action"></a>Azione dell'utente  
  
