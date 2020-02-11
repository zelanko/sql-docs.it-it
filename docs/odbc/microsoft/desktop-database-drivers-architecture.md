---
title: Architettura dei driver di database desktop | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ccd1f14b0cfbcbdbc675a142ebabf11932409832
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071915"
---
# <a name="desktop-database-drivers-architecture"></a>Architettura dei driver di database desktop
Questi driver sono progettati per essere utilizzati in Microsoft Windows 95 o versioni successive o Windows NT 4,0 e Windows 2000. Solo le applicazioni a 32 bit sono supportate in Windows 95 o versioni successive. le applicazioni a 16 bit e a 32 bit sono supportate in Windows NT 4,0 e Windows 2000.  
  
> [!NOTE]  
>  Per informazioni sulla versione di ODBC da utilizzare con questi driver, fare riferimento a *ODBC Programmer ' s Reference*e alle note sulla versione precedenti e correnti. Ad eccezione delle aree indicate, questi driver sono conformi alle informazioni di *riferimento per programmatori ODBC*.  
  
 I driver di database desktop ODBC includono driver a 32 bit per Microsoft Access, dBASE, Microsoft Excel, Paradox e Text. Non sono inclusi driver a 16 bit. (Un driver per Microsoft FoxPro è disponibile separatamente).  
  
 L'architettura dell'applicazione/driver in Windows 95 o versione successiva è:  
  
 ![Architettura del driver&#47;app: Windows 95 e versioni successive](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 L'uso di questi driver da parte di applicazioni a 16 bit in Windows 95 non è supportato.  
  
 L'architettura dell'applicazione/driver in Windows NT 4,0 e Windows 2000 è:  
  
 ![Architettura del driver&#47;app: NT 4,0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 I driver del database desktop sono driver a due livelli. In una configurazione a due livelli, il driver non esegue il processo di analisi, convalida, ottimizzazione ed esecuzione della query. Microsoft Jet esegue invece queste attività. Elabora le chiamate API ODBC e funge da motore SQL. Microsoft Jet è diventato una parte integrante e inseparabile dei driver: viene fornita con i driver e si trova con i driver, anche se nessun'altra applicazione nel computer la utilizza.  
  
 I driver del database desktop sono costituiti da sei driver diversi, o, più precisamente, da un file di driver (ODBCJT32. dll) utilizzato da [Gestione driver](../../odbc/reference/the-driver-manager.md) ODBC in sei modi diversi. Il flag DRIVERID nella voce del registro di sistema per un'origine dati determina il driver in ODBCJT32. dll utilizzato da Gestione driver. Un'applicazione passa questo flag nella stringa di connessione inclusa in una chiamata a **SQLDriverConnect**. Per impostazione predefinita, il flag è l'ID del driver Microsoft Access.  
  
 Il file di installazione driver modifica il flag DRIVERID al momento dell'installazione. A tutti i driver ad eccezione di Microsoft Access driver è associata una DLL di installazione. Quando si fa clic su **installazione** in [Microsoft ODBC Data Source Administrator](../../odbc/admin/odbc-data-source-administrator.md) per un'origine dati, la dll del programma di installazione ODBC (ODBCINST. DLL) carica la dll di installazione. La DLL di installazione Esporta la funzione ODBC Installer **SQLConfigDataSource**. Se un handle di finestra viene passato a **SQLConfigDataSource**, questa funzione Visualizza una finestra di installazione e modifica il flag DRIVERID in base al driver selezionato dall'interfaccia utente.  
  
 Quando un file viene creato a livello di codice, un handle di finestra NULL viene passato a **SQLConfigDataSource**e la funzione crea dinamicamente un'origine dati, modificando il flag DRIVERID in base all'argomento *lpszDriver* nella chiamata di funzione.  
  
 Odbcjt32. dll implementa funzioni ODBC sulla base dell'API Microsoft Jet. Tuttavia, non esiste alcun mapping diretto tra le funzioni ODBC e Microsoft Jet. Molti fattori, ad esempio i modelli di cursore e il mapping SQL, impediscono una correlazione diretta delle funzioni.  
  
 Il driver ODBC risiede tra il motore Microsoft Jet e gestione driver ODBC. Alcune funzioni ODBC chiamate da un'applicazione vengono gestite da Gestione driver e non vengono passate al driver. Per queste funzioni, Microsoft Jet non rileva mai la chiamata di funzione perché non dispone di una connessione diretta a gestione driver.
