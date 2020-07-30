---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: stevestein
ms.author: sstein
ms.openlocfilehash: 636080d7247345cca8f6a6b74fbd19c9e8a487d9
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246156"
---
# <a name="localdb_error_instance_already_shared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Dettagli  
  
| Attributo | valore |
| --------- | ----- |
|Nome prodotto|SQL Server|  
|ID evento|284|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|L'istanza del database locale specificata è già condivisa.|  
  
## <a name="explanation"></a>Spiegazione  
 L'istanza del database locale specificata è già condivisa con un nome condivisione diverso.  
  
## <a name="user-action"></a>Azione dell'utente  
 Annullare la condivisione dell'istanza condivisa prima di condividerla di nuovo con un nome condiviso diverso.  
  
  
