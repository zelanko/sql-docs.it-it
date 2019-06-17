---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3bc344e3e23ce965a2057628e4662ebe41508d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990940"
---
# <a name="localdberrorinstanceexistswithlowerversion"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|258|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|Impossibile creare l'istanza del database locale con la versione specificata. Istanza con lo stesso nome già esistente, ma con una versione inferiore rispetto alla versione specificata.|  
  
## <a name="explanation"></a>Spiegazione  
 Istanza specificata già esistente ma con relativa versione meno recente di quella richiesta.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eliminare l'istanza esistente e ritentare l'operazione.  
  
  
