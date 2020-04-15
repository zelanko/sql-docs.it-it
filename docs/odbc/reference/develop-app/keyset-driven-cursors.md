---
title: Cursori con cursori basati su keyset Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306206"
---
# <a name="keyset-driven-cursors"></a>Cursori gestiti da keyset
Un cursore basato su keyset si trova tra un cursore statico e un cursore dinamico nella sua capacità di rilevare le modifiche. Come un cursore statico, non sempre rileva le modifiche all'appartenenza e all'ordine del set di risultati. Analogamente a un cursore dinamico, rileva le modifiche ai valori delle righe nel set di risultati (soggetto al livello di isolamento della transazione, come impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION).  
  
 Quando viene aperto un cursore basato su keyset, i tasti vengono salvati per l'intero set di risultati; questo corregge l'appartenenza apparente e l'ordine del set di risultati. Mentre il cursore scorre il set di risultati, utilizza le chiavi in questo *keyset* per recuperare i valori dei dati correnti per ogni riga. Si supponga, ad esempio, che un cursore basato su keyset recuperi una riga e un'altra applicazione aggiorni tale riga. Se il cursore recupera nuovamente la riga, i valori che vede sono quelli nuovi perché ha recuperato la riga utilizzando la relativa chiave. Per questo motivo, i cursori basati su keyset rilevano sempre le modifiche apportate da se stessi e da altri.  
  
 Quando il cursore tenta di recuperare una riga che è stata eliminata, questa riga viene visualizzata come un "buco" nel set di risultati: la chiave per la riga esiste nel set di chiavi, ma la riga non esiste più nel set di risultati. Se i valori chiave in una riga vengono aggiornati, la riga viene considerata eliminata e quindi inserita, pertanto tali righe vengono visualizzate anche come fori nel set di risultati. Mentre un cursore basato su keyset può sempre rilevare le righe eliminate da altri, può facoltativamente rimuovere le chiavi per le righe che si elimina dal keyset. I cursori basati su keyset che in questa questa modo non sono in grado di rilevare le proprie eliminazioni. Se un particolare cursore basato su keyset rileva le proprie eliminazioni viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.  
  
 Le righe inserite da altri non sono mai visibili a un cursore basato su keyset perché nel keyset non sono presenti chiavi per queste righe. Tuttavia, un cursore basato su keyset può facoltativamente aggiungere le chiavi per le righe che inserisce se stesso al keyset. I cursori basati su keyset che fanno questo possono rilevare i propri inserti. Se un particolare cursore basato su keyset rileva i propri inserimenti viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.  
  
 La matrice di stato della riga specificata dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR per qualsiasi riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe rilevate come aggiornate, eliminate o inserite.  
  
 I cursori basati su keyset vengono in genere implementati creando una tabella temporanea che contiene le chiavi per ogni riga nel set di risultati. Poiché il cursore deve determinare se le righe sono state aggiornate, questa tabella contiene in genere anche una colonna con informazioni sul controllo delle versioni delle righe.  
  
 Per scorrere il set di risultati originale, il cursore basato su keyset apre un cursore statico sulla tabella temporanea. Per recuperare una riga nel set di risultati originale, il cursore recupera prima la chiave appropriata dalla tabella temporanea e quindi recupera i valori correnti per la riga. Se vengono utilizzati cursori di blocco, il cursore deve recuperare più chiavi e righe.
