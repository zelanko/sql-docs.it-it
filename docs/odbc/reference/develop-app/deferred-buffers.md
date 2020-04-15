---
title: 'Buffer posticipati : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305982"
---
# <a name="deferred-buffers"></a>Buffer posticipati
Un *buffer posticipato* è uno il cui valore viene utilizzato in un determinato momento *dopo* che è stato specificato in una chiamata di funzione. Ad esempio, **SQLBindParameter** viene utilizzato per associare, o *associare,* un buffer di dati con un parametro in un'istruzione SQL. L'applicazione specifica il numero del parametro e passa l'indirizzo, la lunghezza in byte e il tipo del buffer. Il driver salva queste informazioni ma non esamina il contenuto del buffer. Successivamente, quando l'applicazione esegue l'istruzione, il driver recupera le informazioni e le utilizza per recuperare i dati del parametro e inviarli all'origine dati. Pertanto, l'input dei dati nel buffer viene posticipato. Poiché i buffer posticipati vengono specificati in una funzione e utilizzati in un'altra, è un errore di programmazione dell'applicazione per liberare un buffer posticipato mentre il driver prevede ancora che esista; Per ulteriori informazioni, vedere [Allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)più avanti in questa sezione.  
  
 I buffer di input e di output possono essere posticipati. Nella tabella seguente vengono riepilogati gli utilizzi dei buffer posticipati. Si noti che i buffer posticipati associati alle colonne del set di risultati vengono specificati con **SQLBindCol**e i buffer posticipati associati ai parametri dell'istruzione SQL vengono specificati con **SQLBindParameter**.  
  
|Utilizzo del buffer|Type|Specificato con|Usato da|  
|----------------|----------|--------------------|-------------|  
|Invio di dati per i parametri di inputSending data for input parameters|Ingresso posticipato|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Invio di dati da aggiornare o inserire una riga in un set di risultatiSending data to update or insert a row in a result set|Ingresso posticipato|**SQLBindCol**|**SQLSetPos**|  
|Restituzione di dati per i parametri di output e di input/outputReturning data for output and input/output parameters|Output posticipato|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Restituzione dei dati del set di risultatiReturning result set data|Output posticipato|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
