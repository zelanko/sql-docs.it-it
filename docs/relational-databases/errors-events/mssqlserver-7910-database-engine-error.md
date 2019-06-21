---
title: MSSQLSERVER_7910 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7910 (Database Engine error)
ms.assetid: 017a0113-2b17-40b3-a419-30bbc43d46b8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e22a2555f3a7b2e062b370085710e4ba21e74078
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62694585"
---
# <a name="mssqlserver7910"></a>MSSQLSERVER_7910
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|7910|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC2_REPAIR_PAGE_ALLOCATED|  
|Testo del messaggio|Correzione: la pagina P_ID è stata allocata all'oggetto con ID O_ID, indice con ID I_ID, partizione con ID PN_ID, unità allocazione con ID A_ID (tipo TYPE).|  
  
## <a name="explanation"></a>Spiegazione  
Si tratta di un messaggio informativo generato dall'istruzione REPAIR in cui viene indicato che una pagina è stata allocata alla matrice di slot a pagina singola di una mappa di allocazione degli indici (IAM, Index Allocation Map).  
  
## <a name="user-action"></a>Azione dell'utente  
None  
  
