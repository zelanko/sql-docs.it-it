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
manager: craigg
ms.openlocfilehash: e5510eb58315f70195eb40390edec1766c350fb6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468594"
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
  
|Cursore type\action|self|Il proprietario<br /><br /> Txn|Assumere<br /><br /> Txn<br /><br /> (RU[a])|Assumere<br /><br /> Txn<br /><br /> (RC[a])|Assumere<br /><br /> Txn<br /><br /> (RR[a])|Assumere<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Static|||||||  
|Insert|Forse [b]|no|No|No|no|No|  
|Update|Forse [b]|No|no|No|No|No|  
|DELETE|Forse [b]|No|No|No|no|No|  
|Gestito da keyset|||||||  
|Insert|Forse [b]|No|No|no|No|No|  
|Update|Yes|Yes|Yes|Yes|No|no|  
|DELETE|Forse [b]|Yes|Yes|Yes|No|no|  
|Dynamic|||||||  
|Insert|Yes|Yes|Yes|Yes|Yes|No|  
|Update|Yes|Yes|Yes|Yes|No|no|  
|DELETE|Yes|Yes|Yes|Yes|no|No|  
  
 [a] le lettere tra parentesi indicano il livello di isolamento della transazione contenente il cursore. il livello di isolamento della transazione (in cui è stata effettuata la modifica) non è rilevante.  
  
 RU: Read Uncommitted  
  
 RC: Read Committed  
  
 RR: Repeatable Read  
  
 S:  Serializable  
  
 [b] dipende dal modo in cui il cursore viene implementato. Indica se il cursore è possibile rilevare tali modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY **SQLGetInfo**.
