---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec6663028f2c0e133996053a31acfc0e04b49738
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914680"
---
# <a name="mssqlserver2519"></a>MSSQLSERVER_2519
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2519|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_NO_EXPRESSION_EVALUATOR|  
|Testo del messaggio|Impossibile controllare le colonne calcolate e i tipi definiti dall'utente per l'ID di oggetto ID_O (oggetto "NOME_O") perché non è stato possibile inizializzare l'analizzatore di espressioni interno.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio informativo indica che Query Processor non è riuscito a fornire a DBCC un oggetto interno per consentire la restituzione delle colonne calcolate e dei tipi CLR (Common Language Runtime) definiti dall'utente. Ciò significa che non verrà controllata la correttezza delle colonne calcolate e dei tipi CLR definiti dall'utente o che questi non verranno utilizzati durante il controllo DBCC della consistenza tra indici e tabelle di base.  
  
## <a name="user-action"></a>Azione dell'utente  
 None  
  
## <a name="see-also"></a>Vedere anche  
 [MSSQLSERVER_2518](mssqlserver-2518-database-engine-error.md)  
  
  
