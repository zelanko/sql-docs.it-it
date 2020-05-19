---
title: Esecuzione di query (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 597d138832ab5234d0059c25e91fd4d830be255c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711086"
---
# <a name="executing-queries-odbc"></a>Esecuzione di query (ODBC)
  Dopo che un'applicazione ODBC inizializza un handle di connessione e si connette a un'origine dati, alloca uno o più handle di istruzione nell'handle di connessione. L'applicazione può quindi eseguire [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzioni nell'handle di istruzione. Di seguito viene indicata la sequenza generale degli eventi nell'esecuzione di un'istruzione SQL:  
  
1.  Impostare tutti gli attributi di istruzione necessari.  
  
2.  Creare l'istruzione.  
  
3.  Eseguire l'istruzione.  
  
4.  Recuperare tutti i set di risultati.  
  
 Dopo che un'applicazione recupera tutte le righe in tutti i set di risultati restituiti dall'istruzione SQL, può eseguire un'altra query sullo stesso handle di istruzione. Se un'applicazione determina che non è necessario recuperare tutte le righe in un determinato set di risultati, può annullare il resto del set di risultati chiamando [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) o [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
 Se in un'applicazione ODBC è necessario eseguire la stessa istruzione SQL più volte con dati diversi, utilizzare un marcatore di parametro rappresentato da un punto interrogativo (?) nella creazione di un'istruzione SQL:  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 Ogni marcatore di parametro può quindi essere associato a una variabile di programma chiamando [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md).  
  
 Al termine dell'esecuzione di tutte le istruzioni SQL e dell'elaborazione dei relativi set di risultati, l'applicazione rilascia l'handle di istruzione.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta più handle di istruzione per ogni handle di connessione. Le transazioni vengono gestite a livello di connessione, in modo che tutte le operazioni eseguite su tutti gli handle di gestione in un singolo handle di connessione vengano gestite come parte della stessa transazione.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Allocazione di un handle di istruzione](allocating-a-statement-handle.md)  
  
-   [Creazione di un'istruzione SQL &#40;ODBC&#41;](constructing-an-sql-statement-odbc.md)  
  
-   [Costruzione di istruzioni SQL per i cursori](constructing-sql-statements-for-cursors.md)  
  
-   [Utilizzo dei parametri delle istruzioni](using-statement-parameters.md)  
  
-   [Esecuzione di istruzioni &#40;ODBC&#41;](executing-statements/executing-statements-odbc.md)  
  
-   [Rilascio di un handle di istruzione](freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
