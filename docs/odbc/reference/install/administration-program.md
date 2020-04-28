---
title: Programma di amministrazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306642"
---
# <a name="administration-program"></a>Programma di amministrazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 Un programma di amministrazione, l'amministratore ODBC, è incluso in Windows SDK/MDAC SDK. Questo programma e può essere ridistribuito dagli utenti dell'SDK. Inoltre, gli sviluppatori possono scrivere programmi di amministrazione propri. In genere, gli sviluppatori scrivono i propri programmi di amministrazione solo se vogliono mantenere il controllo completo sulla configurazione dell'origine dati o se configurano origini dati direttamente da un'applicazione che funge da programma di amministrazione. Un programma di foglio di calcolo, ad esempio, può consentire agli utenti di aggiungere e quindi utilizzare origini dati in fase di esecuzione.  
  
 Il programma di amministrazione carica prima di tutto la DLL del programma di installazione. Chiama quindi le funzioni nella DLL del programma di installazione per eseguire le attività seguenti:  
  
-   **Aggiungere, modificare o eliminare origini dati in modo interattivo.** Il programma di amministrazione può chiamare **SQLManageDataSources**, **SQLCreateDataSource**o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** Visualizza una finestra di dialogo in cui l'utente può aggiungere, modificare o eliminare origini dati e specificare le opzioni di traccia. Questa funzione viene chiamata quando la DLL del programma di installazione viene richiamata direttamente dal pannello di controllo. **SQLCreateDataSource** Visualizza una finestra di dialogo in cui l'utente può solo aggiungere origini dati. **SQLConfigDataSource** passa la chiamata direttamente alla DLL di installazione del driver.  
  
     In tutti i casi, la DLL del programma di installazione chiama **ConfigDSN** nella DLL di installazione del driver per aggiungere, modificare o eliminare effettivamente l'origine dati. Per ulteriori informazioni, è possibile che la DLL di installazione del driver richieda all'utente.  
  
-   **Aggiungere, modificare o eliminare origini dati in modo invisibile all'utente.** Tramite il programma di amministrazione viene chiamato **SQLConfigDataSource** nella dll del programma di installazione e viene passato un handle di finestra null, il nome di un'origine dati da aggiungere, modificare o eliminare e un elenco di valori per il registro di sistema. La DLL del programma di installazione chiama **ConfigDSN** nella DLL di installazione del driver per aggiungere, modificare o eliminare effettivamente l'origine dati.  
  
-   **Aggiunta, modifica o eliminazione di un'origine dati predefinita.** L'origine dati predefinita è identica a quella di qualsiasi altra origine dati, ad eccezione del fatto che il nome è predefinito. Viene aggiunta, modificata o eliminata allo stesso modo di qualsiasi altra origine dati.
