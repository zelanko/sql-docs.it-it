---
title: "Passaggio 3: Compilare ed eseguire un'istruzione SQL | Microsoft Docs"
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0e369b74ef629c5fd7136b9098f579b5ad2b1b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114255"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Passaggio 3: Compilare ed eseguire un'istruzione SQL
Il terzo passaggio è compilare ed eseguire un'istruzione SQL, come illustrato nella figura seguente. I metodi utilizzati per eseguire questo passaggio sono probabile che variare notevolmente. L'applicazione potrebbe richiedere all'utente di immettere un'istruzione SQL, un'istruzione SQL in base all'input di compilazione o usare un'istruzione SQL a livello di codice. Per altre informazioni, vedere [costruzione di istruzioni SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Mostra la compilazione e l'esecuzione di un'istruzione SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se l'istruzione SQL include parametri, l'applicazione li associa alle variabili di applicazione chiamando **SQLBindParameter** per ogni parametro. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Dopo l'istruzione SQL viene compilata e tutti i parametri sono associati, l'istruzione viene eseguita con **SQLExecDirect**. Se l'istruzione verrà eseguita più volte, può essere preparata con **SQLPrepare** e verranno eseguiti con **SQLExecute**. Per altre informazioni, vedere [esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 L'applicazione potrebbe anche evitare completamente l'esecuzione di un'istruzione SQL e invece chiamare una funzione per restituire un set di risultati contenente informazioni del catalogo, ad esempio le colonne disponibili o tabelle. Per altre informazioni, vedere [Usa i dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Azione successiva dell'applicazione dipende dal tipo di istruzione SQL eseguita.  
  
|Tipo di istruzione SQL|Passare a|  
|---------------------------|----------------|  
|**Selezionare** o del catalogo (funzione)|[Passaggio 4a: Recuperare i risultati](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**UPDATE**, **eliminare**, o **INSERT**|[Passaggio 4b: Recuperare il conteggio delle righe](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Tutte le altre istruzioni SQL|Passaggio 3: Compilare ed eseguire un'istruzione SQL (questo argomento) o [passaggio 5: Eseguire il commit della transazione](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
