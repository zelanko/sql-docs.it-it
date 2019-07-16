---
title: XQuery per la gestione dei dati relazionali | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: ed4583b30ed1e4538a36079f9f7794704b819cda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946162"
---
# <a name="xqueries-handling-relational-data"></a>XQuery per la gestione di dati relazionali
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Si specifica XQuery su un' **xml** colonna di tipo o una variabile utilizzando uno delle [metodi con tipo di dati XML](../t-sql/xml/xml-data-type-methods.md). Questi includono **query ()** , **Value ()** , **exist ()** , oppure **Modify ()** . L'espressione XQuery viene eseguita sull'istanza XML identificata nella query che genera il codice XML.  
  
 Il codice XML generato dall'esecuzione di un'espressione XQuery può includere valori recuperati da altre colonne di set di righe o di variabili Transact-SQL. Per eseguire l'associazione di dati relazionali non XML al codice XML risultante, in SQL Server sono disponibili le pseudofunzioni seguenti come estensioni XQuery:  
  
-   **SQL: Column** (funzione)  
  
-   **SQL: variable** (funzione)  
  
 È possibile usare queste estensioni XQuery quando si specifica un'espressione XQuery nel **query ()** metodo per il **xml** tipo di dati. Di conseguenza, il **query ()** metodo può generare codice XML che combina i dati da XML e non-**xml** i tipi di dati.  
  
 È anche possibile usare queste funzioni quando si usa la **xml** metodi con tipo di dati **Modify ()** , **Value ()** , **query ()** , e  **EXIST ()** per esporre un valore relazionale nell'istanza XML.  
  
 Per altre informazioni, vedere [funzione SQL: Column (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [funzione SQL: variable (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Costruzione di strutture XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
