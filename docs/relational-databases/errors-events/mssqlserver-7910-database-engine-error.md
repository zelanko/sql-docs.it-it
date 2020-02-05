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
ms.openlocfilehash: 8638d205ba3958a88096d12e001a9362bb3d59cb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67951413"
---
# <a name="mssqlserver_7910"></a>MSSQLSERVER_7910
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
nessuno  
  
