---
title: Esecuzione di istruzioni di aggiornamento ed eliminazione posizionate Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307002"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Esecuzione di istruzioni di eliminazione e aggiornamento posizionato
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 Dopo che un'applicazione ha recuperato un blocco di dati con **SQLFetchScroll**, può aggiornare o eliminare i dati nel blocco. Per eseguire un aggiornamento o un'eliminazione posizionata, l'applicazione:  
  
1.  Chiama **SQLSetPos** per posizionare il cursore sulla riga da aggiornare o eliminare.  
  
2.  Costruisce un'istruzione update o delete posizionata con la sintassi seguente:  
  
     **UPDATE** *nome tabella*  
  
     **IDENTIFICATORe** *column-identifier* **=** di colonna SET -*espressione* &#124; **NULL**  
  
     [**,** *identificatore* **=** di colonna e*espressione* &#124; **NULL]**  
  
     **WHERE CURRENT DI** *nome-cursore*  
  
     **DELETE FROM** *nome tabella* WHERE CURRENT **OF** *nome-cursore*  
  
     Il modo più semplice per costruire la clausola **SET** in un'istruzione di aggiornamento posizionato consiste nell'utilizzare gli indicatori di parametro per ogni colonna da aggiornare e utilizzare **SQLBindParameter** per associarli ai buffer del set di righe per la riga da aggiornare. In questo caso, il tipo di dati C del parametro sarà lo stesso tipo di dati C del buffer del set di righe.  
  
3.  Aggiorna i buffer del set di righe per la riga corrente se eseguirà un'istruzione di aggiornamento posizionato. Dopo aver eseguito correttamente un'istruzione di aggiornamento posizionato, la libreria di cursori copia i valori da ogni colonna della riga corrente nella relativa cache.  
  
    > [!CAUTION]  
    >  Se l'applicazione non aggiorna correttamente i buffer del set di righe prima di eseguire un'istruzione di aggiornamento posizionato, i dati nella cache non saranno corretti dopo l'esecuzione dell'istruzione.  
  
4.  Esegue l'istruzione di aggiornamento o eliminazione posizionata utilizzando un'istruzione diversa da quella associata al cursore.  
  
    > [!CAUTION]  
    >  La clausola **WHERE** costruita dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare righe, identificare una riga diversa o identificare più di una riga. Per ulteriori informazioni, vedere [Creazione di istruzioni ricercate](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Tutte le istruzioni di aggiornamento ed eliminazione posizionate richiedono un nome di cursore. Per specificare il nome del cursore, un'applicazione chiama **SQLSetCursorName** prima dell'apertura del cursore. Per utilizzare il nome del cursore generato dal driver, un'applicazione chiama **SQLGetCursorName** dopo l'apertura del cursore.  
  
 Dopo che la libreria di cursori esegue un'istruzione di aggiornamento o eliminazione posizionata, la matrice di stato, i buffer dei set di righe e la cache gestiti dalla libreria di cursori contengono i valori illustrati nella tabella seguente.  
  
|Dichiarazione utilizzata|Valore nella matrice di stato delle righe|Valori in<br /><br /> buffer di set di righeRowset buffers|Valori in<br /><br /> buffer di cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Aggiornamento posizionato|SQL_ROW_UPDATED|Nuovi valori[1]|Nuovi valori[1]|  
|Eliminazione posizionata|SQL_ROW_DELETED|Valori precedenti|Valori precedenti|  
  
 [1] L'applicazione deve aggiornare i valori nei buffer del set di righe prima di eseguire l'istruzione update posizionata; dopo l'esecuzione dell'istruzione update posizionata, la libreria di cursori copia i valori nei buffer del set di righe nella relativa cache.
