---
title: Dati restituiti dalle funzioni del catalogo | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077019"
---
# <a name="data-returned-by-catalog-functions"></a>Dati restituiti dalle funzioni catalogo
Ogni funzione di catalogo restituisce i dati come un set di risultati. Questo set di risultati non è diverso da qualsiasi altro set di risultati. Viene in genere generato da un'istruzione **Select** con parametri predefinita che è hardcoded nel driver o archiviata in una procedura nell'origine dati. Per informazioni sul recupero di dati da un set di risultati, vedere la pagina relativa alla [creazione di un set di risultati](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 Il set di risultati per ogni funzione di catalogo è descritto nella voce di riferimento per tale funzione. Oltre alle colonne elencate, il set di risultati può contenere colonne specifiche del driver dopo l'ultima colonna predefinita. Queste colonne (se presenti) sono descritte nella documentazione del driver.  
  
 Le applicazioni devono associare le colonne specifiche del driver rispetto alla fine del set di risultati. Ovvero, devono calcolare il numero di una colonna specifica del driver come numero dell'ultima colonna recuperata con **SQLNumResultCols** , meno il numero di colonne che si verificano dopo la colonna obbligatoria. In questo modo si evita di dover modificare l'applicazione quando vengono aggiunte nuove colonne al set di risultati nelle future versioni di ODBC o del driver. Per il corretto funzionamento di questo schema, è necessario che i driver aggiungano nuove colonne specifiche del driver prima delle colonne specifiche del driver precedenti, in modo che i numeri delle colonne non cambino rispetto alla fine del set di risultati.  
  
 Gli identificatori restituiti nel set di risultati non sono racchiusi tra virgolette, anche se contengono caratteri speciali. Si supponga, ad esempio, che il carattere virgolette identificatore, che è specifico del driver e restituito tramite **SQLGetInfo**, sia una virgoletta doppia (") e che la tabella contabilità fornitori includa una colonna denominata Customer Name. Nella riga restituita da **SQLColumns** per la colonna, il valore della colonna table_name è accounts pagabile, non "Accounts pagabile" e il valore della colonna column_name è nome cliente, non "Customer Name". Per recuperare i nomi dei clienti nella tabella contabilità fornitori, l'applicazione potrebbe citare i nomi seguenti:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Per ulteriori informazioni, vedere [identificatori delimitati](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Le funzioni di catalogo sono basate su un modello di autorizzazione simile a SQL in cui viene stabilita una connessione in base a un nome utente e una password e vengono restituiti solo i dati per cui l'utente dispone di un privilegio. La protezione delle password dei singoli file, che non rientrano in questo modello, è definita dal driver.  
  
 I set di risultati restituiti dalle funzioni del catalogo non sono quasi mai aggiornabili e le applicazioni non devono essere in grado di modificare la struttura del database modificando i dati in questi set di risultati.
