---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
author: stevestein
ms.author: sstein
ms.openlocfilehash: 488199547cd5b96190b30ab415b08f9be2b4bd66
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641264"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|270|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|Errore durante il recupero del messaggio di errore localizzato. Linguaggio specificato dal parametro 'Language ID' sconosciuto.|  
  
## <a name="explanation"></a>Spiegazione  
 La lingua richiesta per il messaggio di errore di run-time database locale è sconosciuta o non supportata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Provare a richiedere una delle lingue supportate per i messaggi di errore di run-time database locale o una lingua predefinita.  
  
  
