---
title: "Passaggio 3: compilare ed eseguire un'istruzione SQL | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8322cf5e7b4a91bfc5f5f0204cfb25fa4bdad92
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306832"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Passaggio 3: Compilare ed eseguire un'istruzione SQL
Il terzo passaggio consiste nel compilare ed eseguire un'istruzione SQL, come illustrato nella figura seguente. I metodi usati per eseguire questo passaggio possono variare notevolmente. L'applicazione potrebbe richiedere all'utente di immettere un'istruzione SQL, compilare un'istruzione SQL basata sull'input dell'utente oppure utilizzare un'istruzione SQL hardcoded. Per ulteriori informazioni, vedere la pagina relativa alla [costruzione di istruzioni SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Compilazione ed esecuzione di un'istruzione SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se l'istruzione SQL contiene parametri, l'applicazione li associa alle variabili dell'applicazione chiamando **SQLBindParameter** per ogni parametro. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Dopo che l'istruzione SQL è stata compilata ed è stato associato un qualsiasi parametro, l'istruzione viene eseguita con **SQLExecDirect**. Se l'istruzione viene eseguita più volte, può essere preparata con **SQLPrepare** ed eseguita con **SQLExecute**. Per ulteriori informazioni, vedere [esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 L'applicazione potrebbe anche rinunciare all'esecuzione di un'istruzione SQL e chiamare invece una funzione per restituire un set di risultati contenente informazioni sul catalogo, ad esempio le colonne o le tabelle disponibili. Per ulteriori informazioni, vedere [utilizzi dei dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 L'azione successiva dell'applicazione dipende dal tipo di istruzione SQL eseguita.  
  
|Tipo di istruzione SQL|Vai a|  
|---------------------------|----------------|  
|Funzione **Select** o Catalog|[Passaggio 4a: Recuperare i risultati](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**Update**, **Delete**o **Insert**|[Passaggio 4b: Recuperare il conteggio delle righe](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Tutte le altre istruzioni SQL|Passaggio 3: compilare ed eseguire un'istruzione SQL (questo argomento) o [passaggio 5: eseguire il commit della transazione](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
