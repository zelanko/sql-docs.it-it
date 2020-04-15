---
title: "Passaggio 3: Compilare ed eseguire un'istruzione SQL . Documenti Microsoft"
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306832"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Passaggio 3: Compilare ed eseguire un'istruzione SQL
Il terzo passaggio consiste nel compilare ed eseguire un'istruzione SQL, come illustrato nella figura seguente. I metodi utilizzati per eseguire questo passaggio possono variare enormemente. L'applicazione potrebbe richiedere all'utente di immettere un'istruzione SQL, compilare un'istruzione SQL in base all'input dell'utente o utilizzare un'istruzione SQL hardcoded. Per ulteriori informazioni, vedere [Costruzione di istruzioni SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Compilazione ed esecuzione di un'istruzione SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13 (informazioni in questo da systeme pr")  
  
 Se l'istruzione SQL contiene parametri, l'applicazione li associa alle variabili dell'applicazione chiamando **SQLBindParameter** per ogni parametro. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Dopo la compilazione dell'istruzione SQL e l'associazione di tutti i parametri, l'istruzione viene eseguita con **SQLExecDirect**. Se l'istruzione verrà eseguita più volte, può essere preparata con **SQLPrepare** ed eseguita con **SQLExecute**. Per ulteriori informazioni, vedere [Esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 L'applicazione potrebbe anche rinunciare all'esecuzione di un'istruzione SQL e chiamare invece una funzione per restituire un set di risultati contenente informazioni sul catalogo, ad esempio le colonne o le tabelle disponibili. Per ulteriori informazioni, consultate [Usi dei dati del catalogo.](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
 L'azione successiva dell'applicazione dipende dal tipo di istruzione SQL eseguita.  
  
|Tipo di istruzione SQL|Procedere a|  
|---------------------------|----------------|  
|**SELECT** o funzione catalogo|[Passaggio 4a: Recuperare i risultati](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**UPDATE**, **DELETE**o **INSERT**|[Passaggio 4b: Recuperare il conteggio delle righe](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Tutte le altre istruzioni SQL|Passaggio 3: Compilare ed eseguire un'istruzione SQL (questo argomento) o [Passaggio 5: Eseguire il commit della transazioneStep 3:](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md) Build and Execute an SQL Statement (this topic) or Step 5: Commit the Transaction|
