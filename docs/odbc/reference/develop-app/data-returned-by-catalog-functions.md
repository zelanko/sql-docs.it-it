---
title: I dati restituiti dalle funzioni catalogo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14499071bd180a7ea709fda3eb26aeae46f229c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077019"
---
# <a name="data-returned-by-catalog-functions"></a>Dati restituiti dalle funzioni catalogo
Ogni funzione di catalogo restituisce dati come set di risultati. Questo set di risultati non è diverso da qualsiasi altro set di risultati. Viene in genere generato da un oggetto predefinito, con parametri **seleziona** istruzione che è hardcoded nel driver o archiviarlo in una routine nell'origine dati. Per informazioni su come recuperare i dati da un set di risultati, vedere [è stato creato di impostare un risultato?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 Viene descritto il set di risultati per ogni funzione di catalogo nella voce di riferimento per tale funzione. Oltre alle colonne elencate, il set di risultati può contenere colonne specifiche del driver dopo l'ultima colonna predefinito. Queste colonne (se presente) sono descritte nella documentazione del driver.  
  
 Le applicazioni devono essere associati a colonne specifiche del driver relativa alla fine del set di risultati. Vale a dire, si deve calcolare il numero di una colonna specifici del driver come il numero dell'ultima colonna - recuperato con **SQLNumResultCols** - meno il numero di colonne che si verificano dopo la colonna richiesta. In questo modo la necessità di modificare l'applicazione quando vengono aggiunte nuove colonne al risultato impostato nelle future versioni di ODBC o il driver. Per questo schema di funzionamento, i driver devono aggiungere nuove colonne specifiche del driver prima delle colonne specifiche del driver precedente in modo da non modificare i numeri di colonna relativa alla fine del set di risultati.  
  
 Gli identificatori che vengono restituiti nel set di risultati non sono mensili, anche se contengono caratteri speciali. Si supponga ad esempio l'identificatore del tipo di virgolette (che è specifico del driver e viene restituita tramite **SQLGetInfo**) è un segno di virgolette doppie (") e la contabilità fornitori tabella contiene una colonna denominata Customer Name. Nella riga restituita da **SQLColumns** per questa colonna, il valore della colonna TABLE_NAME è contabilità fornitori, non "contabilità", e il valore della colonna COLUMN_NAME è nome del cliente, non "Customer Name". Per recuperare i nomi dei clienti nella tabella di contabilità, l'applicazione potrebbe utilizzare le virgolette questi nomi:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Per altre informazioni, vedere [identificatori racchiusi tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Le funzioni di catalogo si basano su un modello di autorizzazione simile a SQL in cui viene stabilita una connessione basata su nome utente e password e vengono restituiti solo i dati per il quale l'utente dispone di un privilegio. Password di protezione dei singoli file, che non rientrano in questo modello, è definito dal driver.  
  
 I set di risultati restituiti dalle funzioni di catalogo sono quasi mai aggiornabili e le applicazioni non prevede la possibilità di modificare la struttura del database modificando i dati in questi set di risultati.
