---
title: Cursori scorrevoli e isolamento delle transazioni Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304222"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Cursori scorrevoli e isolamento delle transazioni
Nella tabella seguente sono elencati i fattori che regolano la visibilità delle modifiche.  
  
|Modifiche apportate da:|La visibilità dipende da:|  
|----------------------|----------------------------|  
|Cursore|Tipo di cursore, implementazione del cursoreCursor type, cursor implementation|  
|Altri rendiconti nella stessa transazione|Tipo di cursore|  
|Rendiconti in altre transazioni|Tipo di cursore, livello di isolamento delle transazioniCursor type, transaction isolation level|  
  
 Questi fattori sono illustrati nella figura seguente.  
  
 ![Fattori che controllano la visibilità delle modifiche](../../../odbc/reference/develop-app/media/pr23.gif "pr23 (informazioni in stato di pr23")  
  
 Nella tabella seguente viene riepilogata la capacità di ogni tipo di cursore di rilevare le modifiche apportate da se stesso, da altre operazioni nella propria transazione e da altre transazioni. La visibilità di queste ultime modifiche dipende dal tipo di cursore e dal livello di isolamento della transazione contenente il cursore.  
  
|Tipo di cursore: azione|Self|Proprio<br /><br /> Txn|Othr<br /><br /> Txn<br /><br /> (RU[a])|Othr<br /><br /> Txn<br /><br /> (RC[a])|Othr<br /><br /> Txn<br /><br /> (RR[a])|Othr<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Statico|||||||  
|Insert|Forse [b]|No|No|No|No|No|  
|Aggiornamento|Forse [b]|No|No|No|No|No|  
|Delete|Forse [b]|No|No|No|No|No|  
|Gestito da keyset|||||||  
|Insert|Forse [b]|No|No|No|No|No|  
|Aggiornamento|Sì|Sì|Sì|Sì|No|No|  
|Delete|Forse [b]|Sì|Sì|Sì|No|No|  
|Dinamico|||||||  
|Insert|Sì|Sì|Sì|Sì|Sì|No|  
|Aggiornamento|Sì|Sì|Sì|Sì|No|No|  
|Delete|Sì|Sì|Sì|Sì|No|No|  
  
 [a] Le lettere tra parentesi indicano il livello di isolamento della transazione contenente il cursore; il livello di isolamento dell'altra transazione (in cui è stata apportata la modifica) è irrilevante.  
  
 RU: Lettura senza commit  
  
 RC: Lettura impegnata  
  
 RR: Lettura ripetibile  
  
 S: Serializzabile  
  
 [b] Dipende da come viene implementato il cursore. Se il cursore può rilevare tali modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.
