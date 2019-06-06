---
title: I cursori keyset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b349838788a3c442ea9c32fc5b8a7ebbd0240e37
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702082"
---
# <a name="keyset-cursors"></a>Cursori keyset
Il cursore keyset fornisce funzionalità tra un valore statico e un cursore dinamico nella sua capacità di rilevare le modifiche. Come un cursore statico, non sempre rileva le modifiche all'appartenenza e all'ordine del set di risultati. Come un cursore dinamico, rileva le modifiche ai valori delle righe nel set di risultati.  
  
 I cursori gestiti da keyset vengono controllati da un set di identificatori univoci (chiavi), noti come keyset. Le chiavi sono costituite da un set di colonne che identificano in modo univoco le righe del set di risultati. Il keyset corrisponde al set di valori di chiave di tutte le righe restituite dall'istruzione della query.  
  
 Con i cursori gestiti da keyset viene generata e salvata una chiave per ogni riga nel cursore e tale chiave viene archiviata nella workstation client o nel server. Quando si accede a ogni riga, la chiave archiviata viene usata per recuperare i valori correnti dei dati dall'origine dati. In un cursore gestito da keyset, quando il set di chiavi è completamente popolato, l'appartenenza del set di risultati è bloccata. Le aggiunte o gli aggiornamenti successivi che interessano l'appartenenza faranno parte del set di risultati solo quando verrà riaperto.  
  
 Le modifiche ai valori di dati (apportate da altri processi o il proprietario del set di chiavi) sono visibili quando l'utente scorre il set di risultati. Gli inserimenti eseguiti all'esterno del cursore da altri processi sono visibili solo se il cursore viene chiuso e riaperto. Gli inserimenti eseguiti dall'interno del cursore sono visibili alla fine del set di risultati.  
  
 Quando un cursore gestito da keyset tenta di recuperare una riga che è stata eliminata, la riga viene visualizzato come "area libera" nel set di risultati. La chiave per la riga è presente nel keyset, ma la riga non esiste più nel set di risultati. Se vengono aggiornati i valori di chiave in una riga, la riga viene considerata di eliminazione e quindi inserita, tali righe vengono visualizzati anche come buchi del set di risultati. Mentre un cursore gestito da keyset possa sempre rilevare le righe eliminate da altri processi, facoltativamente possibile rimuovere le chiavi per le righe che vengono eliminate se stesso. Gestito da keyset dei cursori che eseguono questa operazione non è in grado di rilevare le righe eliminate perché è stato rimosso l'evidenza.  
  
 Un aggiornamento a una colonna chiave equivale all'eliminazione della chiave precedente seguita da un inserimento della nuova chiave. Il nuovo valore della chiave non è visibile se l'aggiornamento non è stato eseguito tramite il cursore. Se tramite il cursore è stato eseguito l'aggiornamento, il nuovo valore della chiave è visibile alla fine del set di risultati.  
  
 È una variante di cursori definiti cursori a standard gestito da keyset. In un cursore standard basati su keyset, l'appartenenza delle righe nel set di risultati e l'ordine delle righe vengono fissate in tempi di apertura del cursore, ma le modifiche ai valori che vengono apportate dal proprietario del cursore e il commit delle modifiche apportate da altri processi sono visibili. Se una modifica invalida una riga per l'appartenenza o influisce sull'ordine di una riga, la riga non scompare o spostare, a meno che il cursore viene chiuso e riaperto. Dati inseriti non viene visualizzata, ma le modifiche ai dati esistenti vengono visualizzati come il recupero delle righe.  
  
 Il cursore gestito da keyset è difficile da usare in modo corretto perché la sensibilità alle modifiche dei dati dipende da numerose circostanze diverse, come descritto in precedenza. Tuttavia, se l'applicazione non riguarda gli aggiornamenti simultanei, a livello di programmazione possa gestire le chiavi non valide e deve accedere direttamente a determinate righe con chiave, il cursore gestito da keyset potrebbe funzionare per l'utente. Usare la **su adOpenKeyset** per indicare che si desidera utilizzare un cursore keyset in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori forward-Only](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
