---
description: Buffer posticipati
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 320271c39c735eafcfb1d59d26e7d0400eaa6e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424703"
---
# <a name="deferred-buffers"></a>Buffer posticipati
Un *buffer posticipato* è uno il cui valore viene usato in un determinato momento *dopo* che è stato specificato in una chiamata di funzione. Ad esempio, **SQLBindParameter** viene usato per associare, o *associare,* un buffer di dati con un parametro in un'istruzione SQL. L'applicazione specifica il numero del parametro e passa l'indirizzo, la lunghezza in byte e il tipo del buffer. Il driver Salva queste informazioni, ma non esamina il contenuto del buffer. Successivamente, quando l'applicazione esegue l'istruzione, il driver recupera le informazioni e le utilizza per recuperare i dati dei parametri e inviarli all'origine dati. Pertanto, l'input dei dati nel buffer viene posticipato. Poiché i buffer posticipati vengono specificati in una funzione e usati in un altro, si tratta di un errore di programmazione dell'applicazione per liberare un buffer posticipato mentre il driver si aspetta ancora che esista. Per ulteriori informazioni, vedere [allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), più avanti in questa sezione.  
  
 È possibile posticipare sia i buffer di input che quelli di output. Nella tabella seguente sono riepilogati gli utilizzi dei buffer posticipati. Si noti che i buffer posticipati associati alle colonne del set di risultati vengono specificati con **SQLBindCol**e i buffer posticipati associati ai parametri dell'istruzione SQL sono specificati con **SQLBindParameter**.  
  
|Uso del buffer|Type|Specificato con|Usato da|  
|----------------|----------|--------------------|-------------|  
|Invio di dati per i parametri di input|Input posticipato|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Invio di dati per aggiornare o inserire una riga in un set di risultati|Input posticipato|**SQLBindCol**|**SQLSetPos**|  
|Restituzione di dati per parametri di output e di input/output|Output posticipato|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Restituzione di dati del set di risultati|Output posticipato|**SQLBindCol**|**SQLFetch**<br /> **SQLSetPos SQLFetchScroll**|
