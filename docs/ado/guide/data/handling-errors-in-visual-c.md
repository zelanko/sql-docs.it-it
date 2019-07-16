---
title: Gestione degli errori in Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb9eb29a78c3ec5f47e3ff09641ba04ca01d204a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925120"
---
# <a name="handling-errors-in-visual-c"></a>Gestione degli errori in Visual C++
In COM, la maggior parte delle operazioni restituiscono un codice restituito HRESULT che indica se una funzione è stata completata. La direttiva #import genera il codice wrapper intorno a ogni metodo "non elaborato" o una proprietà e controlla il valore HRESULT restituito. Se il valore HRESULT indica un esito negativo, il codice wrapper genera un errore COM da con il codice restituito HRESULT è com_issue_errorex (chiamata) come argomento. Gli oggetti di errore COM possono essere rilevati un **try-catch** blocco. (Per i migliori risultati ottenere, intercettare un riferimento a un oggetto com_error).  
  
 Tenere presente che si tratta di errori ADO: sono il risultato di errore in un'operazione di ADO. Gli errori restituiti dal provider sottostante vengono visualizzati come **errore** gli oggetti nel **connessione** dell'oggetto **errori** raccolta.  
  
 La direttiva #import crea solo le routine di gestione degli errori per i metodi e proprietà dichiarate nella DLL di ADO. Tuttavia, è possibile sfruttare lo stesso meccanismo di gestione degli errori scrivendo il proprio controllo degli errori macro o funzione inline. Vedere l'argomento delle estensioni di Visual C++® per alcuni esempi.
