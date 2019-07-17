---
title: Cursori scorrevoli e isolamento delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3694690ef1cba210da29766e7528762e691f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061606"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Cursori scorrevoli e isolamento delle transazioni
Nella tabella seguente elenca i fattori che controllano la visibilità delle modifiche.  
  
|Modifiche apportate da:|Visibilità dipende da:|  
|----------------------|----------------------------|  
|Cursore|Tipo di cursore, implementazione dei cursori|  
|Altre istruzioni nella stessa transazione|Tipo di cursore|  
|Istruzioni in altre transazioni|Tipo di cursore, a livello di isolamento delle transazioni|  
  
 Questi fattori vengono visualizzati nella figura seguente.  
  
 ![Fattori che controllano la visibilità delle modifiche](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 La tabella seguente riepiloga la capacità di ogni tipo di cursore di rilevare le modifiche apportate da solo da altre operazioni nella propria transazione e da altre transazioni. La visibilità delle modifiche quest'ultime varia a seconda del tipo di cursore e il livello di isolamento della transazione contenente il cursore.  
  
|Cursore type\action|self|Il proprietario<br /><br /> TXN|Assumere<br /><br /> TXN<br /><br /> (RU[a])|Assumere<br /><br /> TXN<br /><br /> (RC[a])|Assumere<br /><br /> TXN<br /><br /> (RR[a])|Assumere<br /><br /> TXN<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Static|||||||  
|Insert|Forse [b]|No|No|No|No|No|  
|Aggiorna|Forse [b]|No|No|No|No|No|  
|Eliminare|Forse [b]|No|No|No|No|No|  
|Gestito da keyset|||||||  
|Insert|Forse [b]|No|No|No|No|No|  
|Aggiorna|Yes|Yes|Yes|Sì|No|No|  
|Eliminare|Forse [b]|Yes|Yes|Sì|No|No|  
|Dynamic|||||||  
|Insert|Yes|Yes|Yes|Yes|Sì|No|  
|Aggiorna|Yes|Yes|Yes|Sì|No|No|  
|Eliminare|Yes|Yes|Yes|Sì|No|No|  
  
 [a] le lettere tra parentesi indicano il livello di isolamento della transazione contenente il cursore. il livello di isolamento della transazione (in cui è stata effettuata la modifica) non è rilevante.  
  
 RU: Read Uncommitted  
  
 RC: Read Committed  
  
 RECORD DI RISORSE: Repeatable Read  
  
 S:  Serializable  
  
 [b] dipende dal modo in cui il cursore viene implementato. Indica se il cursore è possibile rilevare tali modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY **SQLGetInfo**.
