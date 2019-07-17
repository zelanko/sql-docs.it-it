---
title: Gestito da keyset dei cursori | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138837"
---
# <a name="keyset-driven-cursors"></a>Cursori gestiti da keyset
Un cursore gestito da keyset è compresa tra un valore statico e un cursore dinamico nella sua capacità di rilevare le modifiche. Come un cursore statico, non sempre rileva le modifiche all'appartenenza e all'ordine del set di risultati. Un cursore dinamico, è di rilevare le modifiche ai valori delle righe nel set (soggetto a livello di isolamento della transazione, come impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION) di risultati.  
  
 Quando viene aperto un cursore gestito da keyset, Salva le chiavi per l'intero set di risultati; Questa correzione risolve l'apparente appartenenza e l'ordine del set di risultati. Quando il cursore scorre il set di risultati, Usa le chiavi in questo *keyset* per recuperare i valori di dati corrente per ogni riga. Si supponga, ad esempio, un cursore gestito da keyset e recupera una riga e un'altra applicazione, quindi aggiorna tale riga. Se il cursore recupera nuovamente la riga, i valori che rileva sono quelli nuovi poiché refetched la riga tramite la relativa chiave. Per questo motivo, i cursori gestito da keyset sempre rilevano le modifiche apportate da se stessi e ad altri utenti.  
  
 Quando il cursore tenta di recuperare una riga che è stata eliminata, questa riga viene visualizzato come "area libera" nel set di risultati: La chiave per la riga è presente nel keyset, ma la riga non esiste più nel set di risultati. Se vengono aggiornati i valori di chiave in una riga, la riga viene considerata di eliminazione e quindi inserita, tali righe vengono visualizzati anche come buchi del set di risultati. Mentre un cursore gestito da keyset possa sempre rilevare le righe eliminate da altri utenti, facoltativamente possibile rimuovere le chiavi per le righe elimini se stesso dalla keyset. Gestito da keyset dei cursori che eseguono questa operazione non è in grado di rilevare le righe eliminate. Indica se un cursore gestito da keyset particolare rileva la propria eliminazioni viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY **SQLGetInfo**.  
  
 Le righe inserite da altri utenti sono visibili a un cursore gestito da keyset mai perché il set di chiavi è disponibile alcuna chiave delle righe. Tuttavia, un cursore gestito da keyset possa facoltativamente aggiungere le chiavi per le righe viene inserito per il set di chiavi. Gestito da keyset dei cursori che eseguono questa operazione consente di rilevare le proprie istruzioni INSERT. Indica se un cursore gestito da keyset particolare rileva il propria inserimenti viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY **SQLGetInfo**.  
  
 La matrice di stato di riga specificata dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR ogni riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED, SQL_ROW_ADDED per le righe che rileva come aggiornate, eliminate o inserite.  
  
 Gestito da keyset dei cursori vengono implementati comunemente mediante la creazione di una tabella temporanea contenente le chiavi per ogni riga nel set di risultati. Poiché il cursore inoltre è necessario determinare che se sono state aggiornate le righe, questa tabella contiene anche comunemente una colonna con informazioni sul controllo delle versioni delle righe.  
  
 Per scorrere il set di risultati originale, il cursore gestito da keyset viene aperto un cursore statico tramite la tabella temporanea. Per recuperare una riga nel set di risultati originale, il cursore prima di tutto recupera la chiave appropriata dalla tabella temporanea e quindi recupera i valori correnti per la riga. Se si utilizzano cursori a blocchi, il cursore deve recuperare più righe e le chiavi.
