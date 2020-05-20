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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1628522a6ef1c9498ea26e987070ee9f3a873d19
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758847"
---
# <a name="handling-errors-in-visual-c"></a>Gestione degli errori in Visual C++
In COM, la maggior parte delle operazioni restituisce un codice restituito HRESULT che indica se una funzione è stata completata correttamente. La direttiva #import genera il codice wrapper intorno a ogni proprietà o metodo "Raw" e controlla l'HRESULT restituito. Se HRESULT indica un errore, il codice wrapper genera un errore COM chiamando _com_issue_errorex () con il codice restituito HRESULT come argomento. Gli oggetti errore COM possono essere rilevati in un blocco **try-catch** . (Per motivi di efficienza, rilevare un riferimento a un oggetto _com_error).  
  
 Si noti che si tratta di errori ADO: risultanti dall'operazione ADO non riuscita. Gli errori restituiti dal provider sottostante vengono visualizzati come oggetti **Error** nella raccolta **Errors** dell'oggetto **Connection** .  
  
 La direttiva #import crea solo routine di gestione degli errori per metodi e proprietà dichiarati in ADO. dll. Tuttavia, è possibile sfruttare lo stesso meccanismo di gestione degli errori scrivendo una macro o una funzione inline di controllo degli errori personalizzata. Per esempi, vedere l'argomento Visual C++® Extensions.
