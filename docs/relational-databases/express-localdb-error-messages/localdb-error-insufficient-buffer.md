---
description: LOCALDB_ERROR_INSUFFICIENT_BUFFER
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 5c0315eb0d4318fd7e6c82ad19676af37e0391d8
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506198"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Dettagli  
  
| Attributo | Valore |
| --------- | ----- |
|Nome prodotto|SQL Server|  
|ID evento|276|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|Dimensioni del buffer passato al metodo API dell'istanza del database locale non sufficienti.|  
  
## <a name="explanation"></a>Spiegazione  
 Buffer di input troppo corto. Troncamento non necessario.  
  
## <a name="user-action"></a>Azione dell'utente  
 Fornire un buffer con la dimensione specificata.  
  
  
