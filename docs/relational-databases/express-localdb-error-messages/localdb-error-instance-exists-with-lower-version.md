---
description: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5619878edb99204b3b55d99e2a538d662cfb1eb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88409807"
---
# <a name="localdb_error_instance_exists_with_lower_version"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Dettagli  
  
| Attributo | valore |
| --------- | ----- |
|Nome prodotto|SQL Server|  
|ID evento|258|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|Impossibile creare l'istanza del database locale con la versione specificata. Istanza con lo stesso nome già esistente, ma con una versione inferiore rispetto alla versione specificata.|  
  
## <a name="explanation"></a>Spiegazione  
 Istanza specificata già esistente ma con relativa versione meno recente di quella richiesta.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eliminare l'istanza esistente e ritentare l'operazione.  
  
  
