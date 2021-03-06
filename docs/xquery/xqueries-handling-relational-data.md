---
title: Gestione query XQuery dati relazionali | Microsoft Docs
description: 'Informazioni su come associare dati relazionali non XML a XML utilizzando le estensioni XQuery SQL: Column () e SQL: Variable ().'
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
ms.openlocfilehash: 5ebd9c4d2bae1c491d2bd7a23e52c83457942fb6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775475"
---
# <a name="xqueries-handling-relational-data"></a>XQuery per la gestione di dati relazionali
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  È possibile specificare XQuery su una colonna o una variabile di tipo **XML** utilizzando uno dei [metodi con tipo di dati XML](../t-sql/xml/xml-data-type-methods.md). Questi includono **query ()**, **value ()**, **exist ()** o **Modify ()**. L'espressione XQuery viene eseguita sull'istanza XML identificata nella query che genera il codice XML.  
  
 Il codice XML generato dall'esecuzione di un'espressione XQuery può includere valori recuperati da altre colonne di set di righe o di variabili Transact-SQL. Per eseguire l'associazione di dati relazionali non XML al codice XML risultante, in SQL Server sono disponibili le pseudofunzioni seguenti come estensioni XQuery:  
  
-   funzione **SQL: Column ()**  
  
-   funzione **SQL: Variable ()**  
  
 È possibile utilizzare queste estensioni XQuery quando si specifica un'espressione XQuery nel metodo **query ()** del tipo di dati **XML** . Di conseguenza, il metodo **query ()** può produrre codice XML che combina i dati da tipi di dati XML e non**XML** .  
  
 È inoltre possibile utilizzare queste funzioni quando si utilizzano i metodi con tipo di dati **XML** **Modify ()**, **value ()**, **query ()** e **exist ()** per esporre un valore relazionale all'interno di XML.  
  
 Per ulteriori informazioni, vedere funzione [SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [funzione SQL: Variable () (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;di dati XML SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Costrutto XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
