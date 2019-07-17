---
title: Buffer posticipati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076827"
---
# <a name="deferred-buffers"></a>Buffer posticipati
Oggetto *buffer posticipati* è quello il cui valore viene utilizzato in un momento *dopo* è specificato in una chiamata di funzione. Ad esempio, **SQLBindParameter** viene usato per associare, o *associare,* un buffer di dati con un parametro in un'istruzione SQL. L'applicazione specifica il numero del parametro e passa l'indirizzo, lunghezza in byte e il tipo di buffer. Il driver di queste informazioni vengono salvate ma non esamina il contenuto del buffer. In un secondo momento, quando l'applicazione viene eseguita l'istruzione, il driver recupera le informazioni e lo usa per recuperare i dati del parametro e inviarlo all'origine dati. Pertanto, l'input di dati nel buffer viene rinviata. Poiché buffer posticipati sono specificati in una funzione e usato in un altro, è un'applicazione di un errore di programmazione per liberare un buffer posticipato mentre il driver ancora prevede che altri utenti. per altre informazioni, vedere [allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), più avanti in questa sezione.  
  
 È possibile rinviare i buffer di input e di output. Nella tabella seguente sono riepilogati gli utilizzi del buffer posticipati. Si noti che i buffer posticipati associato per le colonne del set di risultati vengono specificati con **SQLBindCol**, e specificati in posticipate i buffer associati ai parametri di istruzione SQL con **SQLBindParameter**.  
  
|Uso di buffer|type|Specificato con|Usato da|  
|----------------|----------|--------------------|-------------|  
|L'invio dei dati per i parametri di input|Input posticipata|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Imposta l'invio dei dati per aggiornare o inserire una riga in un risultato|Input posticipata|**SQLBindCol**|**SQLSetPos**|  
|Restituzione di dati per i parametri di input/output e output|Output posticipato|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Restituzione di risultati di impostare i dati|Output posticipato|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
