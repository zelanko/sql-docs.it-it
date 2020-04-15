---
title: Architettura dei driver di database desktop - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288741"
---
# <a name="desktop-database-drivers-architecture"></a>Architettura dei driver di database desktop
Questi driver sono progettati per l'utilizzo in Microsoft Windows 95 o versione successiva o Windows NT 4.0 e Windows 2000. In Windows 95 o versioni successive sono supportate solo applicazioni a 32 bit; Le applicazioni a 16 e 32 bit sono supportate in Windows NT 4.0 e Windows 2000.  
  
> [!NOTE]  
>  Per informazioni sulla versione di ODBC da utilizzare con questi driver, fare riferimento a *ODBC Programmer's Reference*e alle note sulla versione precedenti e correnti. Ad eccezione delle aree note, questi driver sono conformi a *ODBC Programmer's Reference*.  
  
 I driver di database desktop ODBC includono driver a 32 bit per Microsoft Access, dBASE, Microsoft Excel, Paradox e Text. Non sono inclusi driver a 16 bit. (Un driver per Microsoft FoxPro è disponibile separatamente.)  
  
 L'architettura dell'applicazione/driver in Windows 95 o versioni successive è:  
  
 ![Architettura dei driver di&#47;delle app: Windows 95 e versioni successive](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 L'utilizzo di questi driver da parte di applicazioni a 16 bit in Windows 95 non è supportato.  
  
 L'architettura dell'applicazione/driver in Windows NT 4.0 e Windows 2000 è:  
  
 ![Architettura dei driver di&#47;delle app: NT 4.0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2 (informazioni in base alla criminalità con un'")  
  
 I driver di database desktop sono driver a due livelli. In una configurazione a due livelli, il driver non esegue il processo di analisi, convalida, ottimizzazione ed esecuzione della query. Al contrario, Microsoft Jet esegue queste attività. Elabora le chiamate all'API ODBC e funge da motore SQL. Microsoft Jet è diventato parte integrante e inseparabile dei driver: viene fornito con i driver e risiede con i driver, anche se nessun'altra applicazione sul computer lo utilizza.  
  
 I driver di Database desktop sono costituiti da sei driver diversi, o, più precisamente, da un file driver (Odbcjt32.dll) che [Gestione driver](../../odbc/reference/the-driver-manager.md) ODBC utilizza in sei modi diversi. Il flag DRIVERID nella voce del Registro di sistema per un'origine dati determina quale driver in Odbcjt32.dll utilizza Gestione Driver. Un'applicazione passa questo flag nella stringa di connessione inclusa in una chiamata a **SQLDriverConnect**. Per impostazione predefinita, il flag è l'ID del driver di Microsoft Access.  
  
 Il file di installazione del driver modifica il flag DRIVERID al momento dell'installazione. A tutti i driver ad eccezione del driver di Microsoft Access è associata una DLL di installazione. Quando si fa clic su **Installazione** in [Amministrazione origine dati Microsoft ODBC](../../odbc/admin/odbc-data-source-administrator.md) per un'origine dati, la DLL del programma di installazione ODBC (Odbcinst.dll) carica la DLL di installazione. La DLL di installazione esporta la funzione del programma di installazione ODBC **SQLConfigDataSource**. Se un handle di finestra viene passato a **SQLConfigDataSource**, questa funzione visualizza una finestra di installazione e modifica il flag DRIVERID in base al driver selezionato dall'interfaccia utente.  
  
 Quando un file viene creato a livello di codice, un handle di finestra NULL viene passato a **SQLConfigDataSource**e la funzione crea un'origine dati in modo dinamico, modificando il driverID flag in base all'argomento *lpszDriver* nella chiamata di funzione.  
  
 Odbcjt32.dll implementa le funzioni ODBC sopra l'API Microsoft Jet. Non esiste tuttavia un mapping diretto tra le funzioni ODBC e Microsoft Jet. Molti fattori, ad esempio i modelli di cursore e il mapping SQL, impediscono una correlazione diretta delle funzioni.  
  
 Il driver ODBC si trova tra il modulo di gestione Microsoft Jet e Gestione driver ODBC. Alcune funzioni ODBC chiamate da un'applicazione vengono gestite da Gestione Driver e non passate al driver. Per queste funzioni, Microsoft Jet non vede mai la chiamata di funzione perché non dispone di una connessione diretta a Gestione Driver.
