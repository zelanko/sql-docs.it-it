---
title: Architettura dei driver di Database desktop | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7487d073b95190418ee7f6900390a2d60ce42e13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629052"
---
# <a name="desktop-database-drivers-architecture"></a>Architettura dei driver di database desktop
Questi driver sono progettati per l'uso in Microsoft Windows 95 o versioni successive, o Windows NT 4.0 e Windows 2000. Sono supportate solo le applicazioni a 32 bit in Windows 95 o versione successiva. le applicazioni a 16 bit e a 32 bit sono supportate in Windows NT 4.0 e Windows 2000.  
  
> [!NOTE]  
>  Per informazioni sulla versione di ODBC da utilizzare con questi driver, vedere la *riferimento per programmatori ODBC*e note sulla versione precedenti e correnti. Fatta eccezione per le aree indicate, questi driver conformi al *riferimento per programmatori ODBC*.  
  
 I driver di Database Desktop ODBC includere driver a 32 bit per Microsoft Access, dBASE, Microsoft Excel, Paradox e testo. No. 16 - bit driver sono inclusi. (Un driver per Microsoft FoxPro è disponibile separatamente).  
  
 L'architettura applicazione/driver in Windows 95 o versione successiva è:  
  
 ![App&#47;architettura del driver: Windows 95 e versioni successive](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Non è supportato l'uso di questi driver per applicazioni a 16 bit in Windows 95.  
  
 L'architettura applicazione/driver in Windows NT 4.0 e Windows 2000 è:  
  
 ![App&#47;architettura del driver: NT 4.0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 I driver di Database Desktop sono i driver a due livelli. In una configurazione a due livelli, il driver non esegue il processo di analisi, convalida, ottimizzare e l'esecuzione della query. Al contrario, Microsoft Jet esegue queste attività. Elabora chiamate all'API ODBC e agisce come un motore SQL. Microsoft Jet è diventata una parte integrante e Inseparabile del driver: Viene fornito con i driver e si trova con i driver, anche se nessun altra applicazione nel computer lo usa.  
  
 I driver di Database Desktop è costituito da sei diversi driver - o, più precisamente, un file del driver (Odbcjt32.dll) che ODBC [gestione Driver](../../odbc/reference/the-driver-manager.md) utilizza in sei modi diversi. Il flag DRIVERID nella voce del Registro di sistema per un'origine dati determina quali driver in Odbcjt32.dll Usa gestione Driver. Un'applicazione passa questo flag nella stringa di connessione inclusa in una chiamata a **SQLDriverConnect**. Per impostazione predefinita, il flag è l'ID del driver Microsoft Access.  
  
 Il file di installazione di driver modifica il flag DRIVERID in fase di installazione. Tutti i driver tranne il driver Microsoft Access dispone di una DLL di installazione associato. Quando fa clic su **programma di installazione** nel [Amministrazione origine dati ODBC di Microsoft](../../odbc/admin/odbc-data-source-administrator.md) per un'origine dati, il programma di installazione ODBC DLL (Odbccp32.dll) consente di caricare la DLL di installazione. La DLL di installazione consente di esportare la funzione di programma di installazione ODBC **SQLConfigDataSource**. Se un handle di finestra viene passato a **SQLConfigDataSource**, questa funzione consente di visualizzare una finestra del programma di installazione e il flag DRIVERID in base al driver selezionato dall'interfaccia utente viene modificato.  
  
 Quando viene creato un file a livello di programmazione, un handle di finestra NULL viene passato al **SQLConfigDataSource**, e la funzione crea un'origine dati in modo dinamico, il flag DRIVERID in base alla modifica di *lpszDriver*argomento nella chiamata di funzione.  
  
 ODBCJT32.dll implementa funzioni ODBC oltre all'API di Microsoft Jet. Non c'è alcun mapping diretto tra le funzioni ODBC e Microsoft Jet, tuttavia. Molti fattori, ad esempio i modelli di cursore e il mapping di SQL, impediscono una correlazione diretta delle funzioni.  
  
 Il driver ODBC si trova tra il motore Jet di Microsoft e di gestione Driver ODBC. Alcune funzioni ODBC chiamati da un'applicazione vengono gestite da Gestione Driver e non è stati passati al driver. Per queste funzioni, Microsoft Jet non vede mai la funzione chiamata perché non dispone di una connessione diretta da Gestione Driver.
