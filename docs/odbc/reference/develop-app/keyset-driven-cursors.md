---
title: Cursori gestiti da keyset | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c40fe8c823115c3131a1719185bce8f1506df81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138837"
---
# <a name="keyset-driven-cursors"></a>Cursori gestiti da keyset
Un cursore gestito da keyset si trova tra un cursore statico e un cursore dinamico nella capacità di rilevare le modifiche. Come un cursore statico, non sempre rileva le modifiche all'appartenenza e all'ordine del set di risultati. Analogamente a un cursore dinamico, rileva le modifiche apportate ai valori delle righe nel set di risultati, in base al livello di isolamento della transazione, impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION.  
  
 Quando viene aperto un cursore gestito da keyset, Salva le chiavi per l'intero set di risultati; Questa operazione corregge l'appartenenza e l'ordine del set di risultati. Quando il cursore scorre il set di risultati, USA le chiavi in questo *Keyset* per recuperare i valori dei dati correnti per ogni riga. Si supponga, ad esempio, che un cursore gestito da keyset recuperi una riga e un'altra applicazione aggiorni la riga. Se il cursore Recupera la riga, i valori rilevati sono quelli nuovi perché la riga è stata rirecuperata usando la relativa chiave. Per questo motivo, i cursori gestiti da keyset rilevano sempre le modifiche apportate da soli e da altri.  
  
 Quando il cursore tenta di recuperare una riga che è stata eliminata, questa riga viene visualizzata come "Hole" nel set di risultati: la chiave per la riga esiste nel keyset, ma la riga non esiste più nel set di risultati. Se vengono aggiornati i valori di chiave in una riga, la riga viene considerata eliminata e quindi inserita, quindi tali righe vengono visualizzate anche come buchi nel set di risultati. Mentre un cursore gestito da keyset è sempre in grado di rilevare le righe eliminate da altri, può facoltativamente rimuovere le chiavi per le righe che elimina dal keyset. I cursori gestiti da keyset che non sono in grado di rilevare le proprie eliminazioni. Il fatto che un determinato cursore gestito da keyset rilevi le proprie eliminazioni viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.  
  
 Le righe inserite da altri non sono mai visibili a un cursore gestito da keyset perché nel keyset non esiste alcuna chiave per queste righe. Tuttavia, un cursore gestito da keyset può facoltativamente aggiungere le chiavi per le righe che inserisce automaticamente nel keyset. I cursori gestiti da keyset che consentono di rilevare i propri inserimenti. Il fatto che un determinato cursore gestito da keyset rilevi i propri inserimenti viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.  
  
 La matrice di stato della riga specificata dall'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR per qualsiasi riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe rilevate come aggiornate, eliminate o inserite.  
  
 I cursori gestiti da keyset vengono in genere implementati creando una tabella temporanea che contiene le chiavi per ogni riga del set di risultati. Poiché il cursore deve inoltre determinare se le righe sono state aggiornate, in genere la tabella contiene anche una colonna con informazioni sul controllo delle versioni delle righe.  
  
 Per scorrere il set di risultati originale, il cursore gestito da keyset apre un cursore statico sulla tabella temporanea. Per recuperare una riga nel set di risultati originale, il cursore recupera prima la chiave appropriata dalla tabella temporanea e quindi recupera i valori correnti per la riga. Se si utilizzano cursori a blocchi, il cursore deve recuperare più chiavi e righe.
