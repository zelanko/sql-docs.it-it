---
title: 'Appendice F: libreria di cursori ODBC Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292431"
---
# <a name="appendix-f-odbc-cursor-library"></a>Appendice F: Libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori ODBC (Odbccr32.dll) supporta i cursori scorrevoli a blocchi per qualsiasi driver conforme al livello di conformità api di livello 1 e che può essere ridistribuito dagli sviluppatori con le applicazioni o i driver. La libreria di cursori supporta inoltre le istruzioni di aggiornamento ed eliminazione posizionate per i set di risultati generati dalle istruzioni **SELECT.** Sebbene supporti solo i cursori statici e forward-only, la libreria di cursori soddisfa le esigenze di molte applicazioni. Inoltre, può fornire buone prestazioni, soprattutto per set di risultati di piccole e medie dimensioni e per le applicazioni che non dispongono di un buon supporto per i cursori.  
  
 La libreria di cursori è una libreria a collegamento dinamico (DLL) che si trova tra Gestione Driver e il driver. Quando un'applicazione chiama una funzione, Gestione Driver chiama la funzione nella libreria di cursori, che esegue la funzione o la chiama nel driver specificato. Per una determinata connessione, un'applicazione specifica se la libreria di cursori viene sempre utilizzata, utilizzata se il driver non supporta i cursori scorrevoli o non viene mai utilizzato.  
  
 La libreria di cursori viene visualizzata come driver di Gestione Driver. Se la libreria di cursori si trova tra Gestione Driver e un driver ODBC *2.x,* la libreria di cursori viene visualizzata come un driver ODBC *2.x.* Se la libreria di cursori si trova tra Gestione Driver e un driver ODBC *3.x,* la libreria di cursori viene visualizzata come un driver ODBC *3.x.* Il comportamento esposto dalla libreria di cursori dipende dalla versione del driver che sta utilizzando, ad eccezione degli offset di associazione, che è supportato per entrambi i driver ODBC *2.x* e ODBC *3.x.*  
  
 Per implementare i cursori a blocchi in **SQLFetch** e **SQLFetchScroll**, la libreria di cursori chiama ripetutamente **SQLFetch** nel driver. Per implementare lo scorrimento, memorizza nella cache i dati recuperati in memoria e nei file su disco. Quando un'applicazione richiede un nuovo set di righe, la libreria di cursori lo recupera in base alle esigenze dal driver o dalla cache.  
  
 Per implementare istruzioni di aggiornamento ed eliminazione posizionate, la libreria di cursori crea un'istruzione **UPDATE** o **DELETE** con una clausola **WHERE** che specifica il valore memorizzato nella cache di ogni colonna associata nella riga. Quando esegue un'istruzione update posizionata, la libreria di cursori aggiorna la cache dai valori nei buffer del set di righe.  
  
 Per ulteriori informazioni sulla libreria di cursori ODBC, vedere le sezioni seguenti di questa appendice:  
  
-   [Uso della libreria di cursori ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Esecuzione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Esempio di codice della libreria di cursori](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Note di implementazione](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Codici di errore della libreria di cursori ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
