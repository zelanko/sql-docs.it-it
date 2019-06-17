---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb60bfa05e75c06b7da04042aa1abfbd42b756c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761901"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|7915|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Testo del messaggio|Correzione: Catena IAM per l'oggetto con ID O_ID, indice con ID I_ID, partizione con ID PN_ID, unità allocazione con ID A_ID (tipo TYPE), è stata troncata prima della pagina P_ID e verrà ricompilato.|  
  
## <a name="explanation"></a>Spiegazione  
 Si tratta di un messaggio informativo inviato da REPAIR che indica che la catena IAM (Index Allocation Map) specificata è stata corretta in modo da essere ricompilata. Per la correzione può essere necessaria l'allocazione di un nuovo inizio della catena IAM o la rimozione delle pagine danneggiate dalla catena.  
  
## <a name="user-action"></a>Azione dell'utente  
 None  
  
  
