---
title: 'Appendice F: Libreria di cursori ODBC | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a87f6c365762f5b262dfbed07bbae14cb08604a
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794147"
---
# <a name="appendix-f-odbc-cursor-library"></a>Appendice F: Libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 La libreria di cursori ODBC (Odbccr32) supporta i cursori scorrevoli di blocco per qualsiasi driver conforme con il livello di conformità di livello 1 API e può essere ridistribuita dagli sviluppatori con applicazioni o driver. La libreria di cursori supporta anche istruzioni di eliminazione e aggiornamento posizionato per set di risultati generati da **seleziona** istruzioni. Anche se supporta solo cursori statici e forward-only, la libreria di cursori soddisfa le esigenze di molte applicazioni. Inoltre, può fornire buone prestazioni, soprattutto per set di risultati di dimensioni piccole o medie dimensioni e per le applicazioni che non è supportata buona cursore.  
  
 La libreria di cursori è una libreria di collegamento dinamico (DLL) che risiede tra gestione Driver e il driver. Quando un'applicazione chiama una funzione, gestione Driver chiama la funzione nella libreria di cursori, che esegue la funzione o chiama tale driver specificato. Per una determinata connessione, un'applicazione specifica se la libreria di cursori viene sempre usata, utilizzata se il driver non supporta i cursori scorrevoli o mai utilizzata.  
  
 La libreria di cursori viene visualizzato come un driver per la gestione di Driver. Se la libreria di cursori si trova tra la gestione di Driver e un database ODBC *2.x* driver, la libreria di cursori viene visualizzato come un database ODBC *2.x* driver. Se la libreria di cursori si trova tra la gestione di Driver e un database ODBC *3.x* driver, la libreria di cursori viene visualizzato come un database ODBC *3.x* driver. Comportamento anomalo dalla libreria di cursori varia a seconda della versione del driver può essere utilizzato con, fatta eccezione per gli offset di associazione, che è supportato per entrambi ODBC *2.x* e ODBC *3.x* driver.  
  
 Per implementare cursori a blocchi nei **SQLFetch** e **SQLFetchScroll**, la libreria di cursori chiama ripetutamente **SQLFetch** nel driver. Per implementare lo scorrimento, memorizza nella cache i dati che sono recuperati nella memoria e nei file di disco. Quando un'applicazione richiede un nuovo set di righe, la libreria di cursori recupera in base alle esigenze dal driver o dalla cache.  
  
 Per implementare l'aggiornamento posizionato ed eliminare le istruzioni, la libreria di cursori costruisce un **aggiornare** oppure **eliminare** istruzione con un **in cui** clausola che specifica memorizzato nella cache valore di ogni colonna associata nella riga. Quando viene eseguita un'istruzione di aggiornamento posizionato, la libreria di cursori Aggiorna la cache da quelli nei buffer di set di righe.  
  
 Per altre informazioni sulla libreria di cursori ODBC, vedere le sezioni seguenti di questa appendice:  
  
-   [Uso della libreria di cursori ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Esecuzione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Esempio di codice della libreria di cursori](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Note di implementazione](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Codici di errore della libreria di cursori ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
