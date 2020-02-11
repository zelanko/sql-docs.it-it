---
title: Parametri dell'istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f3aad1537475e288cff06725b5dbd0fe2383924
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107237"
---
# <a name="statement-parameters"></a>Parametri delle istruzioni
Un *parametro* è una variabile in un'istruzione SQL. Si supponga, ad esempio, che una tabella Parts includa colonne denominate PartId, Description e price. Per aggiungere una parte senza parametri, è necessario creare un'istruzione SQL, ad esempio:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Sebbene questa istruzione inserisca un nuovo ordine, non è una soluzione appropriata per un'applicazione Order Entry perché i valori da inserire non possono essere hardcoded nell'applicazione. In alternativa, è possibile costruire l'istruzione SQL in fase di esecuzione, utilizzando i valori da inserire. Questa non è anche una soluzione corretta, a causa della complessità della creazione di istruzioni in fase di esecuzione. La soluzione migliore consiste nel sostituire gli elementi della clausola **values** con i punti interrogativi (?) o i *marcatori di parametro*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Gli indicatori di parametro vengono quindi associati a variabili dell'applicazione. Per aggiungere una nuova riga, l'applicazione deve solo impostare i valori delle variabili ed eseguire l'istruzione. Il driver recupera quindi i valori correnti delle variabili e li invia all'origine dati. Se l'istruzione viene eseguita più volte, l'applicazione può rendere il processo ancora più efficiente preparando l'istruzione.  
  
 L'istruzione appena mostrata potrebbe essere hardcoded in un'applicazione Order entry per inserire una nuova riga. Tuttavia, i marcatori di parametro non sono limitati alle applicazioni verticali. Per qualsiasi applicazione, semplificano la creazione di istruzioni SQL in fase di esecuzione evitando conversioni da e verso il testo. Ad esempio, l'ID della parte appena mostrato è probabilmente archiviato nell'applicazione come numero intero. Se l'istruzione SQL viene costruita senza marcatori di parametro, l'applicazione deve convertire l'ID della parte in testo e l'origine dati deve convertirla di nuovo in un valore integer. Utilizzando un marcatore di parametro, l'applicazione può inviare l'ID parte al driver come intero, che in genere può inviarlo all'origine dati come valore integer. In questo modo vengono salvate due conversioni. Per i valori di dati Long, questo è molto importante, perché i formati di testo di tali valori superano spesso la lunghezza consentita di un'istruzione SQL.  
  
 I parametri sono validi solo in determinate posizioni nelle istruzioni SQL. Ad esempio, non sono consentiti nell'elenco di selezione, ovvero l'elenco di colonne che devono essere restituite da un'istruzione **Select** , né sono consentiti come operandi di un operatore binario come il segno di uguale (=), perché sarebbe impossibile determinare il tipo di parametro. In genere, i parametri sono validi solo nelle istruzioni DML (Data Manipulation Language) e non nelle istruzioni DDL (Data Definition Language). Per ulteriori informazioni, vedere [marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md) nell'Appendice C: grammatica SQL.  
  
 Quando l'istruzione SQL richiama una stored procedure, è possibile utilizzare i parametri denominati. I parametri denominati sono identificati dai rispettivi nomi, non dalla relativa posizione nell'istruzione SQL. Possono essere associati tramite una chiamata a **SQLBindParameter**, ma il parametro viene identificato dal campo SQL_DESC_NAME del valore dpi (descrittore del parametro di implementazione), non dall'argomento *ParameterNumber* di **SQLBindParameter**. Possono anche essere associati chiamando **SQLSetDescField** o **SQLSetDescRec**. Per ulteriori informazioni sui parametri denominati, vedere [associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), più avanti in questa sezione. Per ulteriori informazioni sui descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di parametri](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurazione dei valori dei parametri](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parametri di procedure](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
