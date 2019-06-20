---
title: L'esecuzione di istruzioni di eliminazione e aggiornamento posizionato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2391c01d93c876562ab9d870ab0dba22bf74cea5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63189021"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Esecuzione di istruzioni di eliminazione e aggiornamento posizionato
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Dopo che un'applicazione ha recuperato un blocco di dati con **SQLFetchScroll**, può aggiornare o eliminare i dati nel blocco. Per eseguire un aggiornamento posizionato o delete, l'applicazione:  
  
1.  Le chiamate **SQLSetPos** per posizionare il cursore sulla riga deve essere aggiornato o eliminato.  
  
2.  Costruisce un aggiornamento posizionato o istruzione delete con la sintassi seguente:  
  
     **UPDATE** *-nome della tabella*  
  
     **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
     [ **,** *column-identifier* **=** {*expression* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *-nome del cursore*  
  
     **DELETE FROM** *nome tabella* **WHERE CURRENT OF** *-nome del cursore*  
  
     Il modo più semplice per costruire il **impostata** clausola in un'istruzione di aggiornamento posizionato consiste nell'usare i marcatori di parametro per ogni colonna da aggiornare e usare **SQLBindParameter** da associare al buffer di set di righe per il riga da aggiornare. In questo caso, il tipo di dati C del parametro sarà quello utilizzato per il tipo di dati C del buffer di righe.  
  
3.  Consente di aggiornare i buffer di righe per la riga corrente se eseguirlo un'istruzione per gli aggiornamenti posizionati. Dopo aver eseguito correttamente un'istruzione di aggiornamento posizionato, la libreria di cursori copia i valori di ogni colonna nella riga corrente nella relativa cache.  
  
    > [!CAUTION]  
    >  Se l'applicazione non aggiornano correttamente il buffer di set di righe prima di eseguire un'istruzione di aggiornamento posizionato, i dati nella cache non saranno corretto dopo l'esecuzione dell'istruzione.  
  
4.  Esegue l'aggiornamento posizionato o istruzione delete tramite un'istruzione diversa rispetto all'istruzione associato al cursore.  
  
    > [!CAUTION]  
    >  Il **in cui** clausola costruito dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare tutte le righe, identificare una riga diversa o per identificare più di una riga. Per altre informazioni, vedere [costruzione di istruzioni di eseguire la ricerca](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Tutti posizionato aggiornamento e istruzioni di eliminazione richiedono un nome di cursore. Per specificare il nome del cursore, un'applicazione chiama **SQLSetCursorName** prima dell'apertura del cursore. Per usare il nome di cursore generato dal driver, un'applicazione chiama **SQLGetCursorName** dopo l'apertura del cursore.  
  
 Dopo il cursore libreria esegue un aggiornamento posizionato o istruzione delete, la matrice di stato, i buffer di righe e cache gestita dalla libreria di cursori contengono i valori mostrati nella tabella seguente.  
  
|Istruzione utilizzata|Valore nella matrice di stato riga|Valori in<br /><br /> buffer di righe|Valori in<br /><br /> buffer di cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Aggiornamento posizionato|SQL_ROW_UPDATED|Nuovi valori di [1]|Nuovi valori di [1]|  
|Delete posizionata|SQL_ROW_DELETED|Valori precedenti|Valori precedenti|  
  
 [1] l'applicazione deve aggiornare i valori nei buffer di set di righe prima di eseguire l'istruzione per gli aggiornamenti posizionati. Dopo l'esecuzione dell'istruzione di aggiornamento posizionato, la libreria di cursori copia i valori nei buffer di set di righe per la propria cache.
