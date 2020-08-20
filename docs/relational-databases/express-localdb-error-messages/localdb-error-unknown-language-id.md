---
description: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
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
ms.openlocfilehash: bc5e696b75b1f1a011c380d77010ca3167187a3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470545"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Dettagli  
  
| Attributo | valore |
| --------- | ----- |
|Nome prodotto|SQL Server|  
|ID evento|270|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|Errore durante il recupero del messaggio di errore localizzato. Linguaggio specificato dal parametro 'Language ID' sconosciuto.|  
  
## <a name="explanation"></a>Spiegazione  
 La lingua richiesta per il messaggio di errore di run-time database locale è sconosciuta o non supportata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Provare a richiedere una delle lingue supportate per i messaggi di errore di run-time database locale o una lingua predefinita.  
  
  
