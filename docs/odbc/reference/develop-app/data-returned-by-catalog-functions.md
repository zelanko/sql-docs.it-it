---
title: Dati restituiti dalle funzioni di catalogo Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305230"
---
# <a name="data-returned-by-catalog-functions"></a>Dati restituiti dalle funzioni catalogo
Ogni funzione di catalogo restituisce i dati come set di risultati. Questo set di risultati non è diverso da qualsiasi altro set di risultati. Viene in genere generata da un'istruzione **SELECT** predefinita con parametri che è hardcoded nel driver o archiviata in una procedura nell'origine dati. Per informazioni su come recuperare dati da un set di risultati, vedere È stato creato un set di [risultati?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 Il set di risultati per ogni funzione di catalogo è descritto nella voce di riferimento per tale funzione. Oltre alle colonne elencate, il set di risultati può contenere colonne specifiche del driver dopo l'ultima colonna predefinita. Queste colonne (se presenti) sono descritte nella documentazione del driver.  
  
 Le applicazioni devono associare colonne specifiche del driver rispetto alla fine del set di risultati. Ovvero, è necessario calcolare il numero di una colonna specifica del driver come numero dell'ultima colonna , recuperata con **SQLNumResultCols** , meno il numero di colonne che si verificano dopo la colonna richiesta. Ciò consente di evitare di dover modificare l'applicazione quando vengono aggiunte nuove colonne al set di risultati nelle versioni future di ODBC o il driver. Affinché questo schema funzioni, i driver devono aggiungere nuove colonne specifiche del driver prima delle colonne specifiche del driver precedenti in modo che i numeri di colonna non cambino rispetto alla fine del set di risultati.  
  
 Gli identificatori restituiti nel set di risultati non sono racchiusi tra virgolette, anche se contengono caratteri speciali. Si supponga, ad esempio, che il carattere dell'virgoletta dell'identificatore (che è specifico del driver e restituito tramite **SQLGetInfo**) sia una virgoletta doppia (") e che la tabella Contabilità fornitori contenga una colonna denominata Nome cliente. Nella riga restituita da **SQLColumns** per questa colonna, il valore della colonna TABLE_NAME è Contabilità fornitori, non "Contabilità fornitori", e il valore della colonna COLUMN_NAME è Nome cliente, non "Nome cliente". Per recuperare i nomi dei clienti nella tabella Contabilità fornitori, l'applicazione cita questi nomi:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Per ulteriori informazioni, vedere [Identificatori tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Le funzioni di catalogo sono basate su un modello di autorizzazione di tipo SQL in cui viene stabilita una connessione in base a un nome utente e una password e vengono restituiti solo i dati per i quali l'utente dispone di un privilegio. La protezione con password dei singoli file, che non rientra in questo modello, è definita dal driver.  
  
 I set di risultati restituiti dalle funzioni di catalogo non sono quasi mai aggiornabili e le applicazioni non dovrebbero aspettarsi di poter modificare la struttura del database modificando i dati in questi set di risultati.
