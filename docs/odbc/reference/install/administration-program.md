---
title: Programma di Amministrazione Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306642"
---
# <a name="administration-program"></a>Programma di amministrazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 Un programma di amministrazione, l'Amministratore ODBC, è incluso in Windows SDK/MDAC SDK. Questo programma e può essere ridistribuito dagli utenti dell'SDK. Inoltre, gli sviluppatori possono scrivere i propri programmi di amministrazione. In genere, gli sviluppatori scrivono i propri programmi di amministrazione solo se desiderano mantenere il controllo completo sulla configurazione dell'origine dati o se stanno configurando le origini dati direttamente da un'applicazione che funge da programma di amministrazione. Ad esempio, un programma per fogli di calcolo potrebbe consentire agli utenti di aggiungere e quindi utilizzare origini dati in fase di esecuzione.  
  
 Il programma di amministrazione carica innanzitutto la DLL del programma di installazione. Chiama quindi le funzioni nella DLL del programma di installazione per eseguire le attività seguenti:  
  
-   **Aggiungere, modificare o eliminare origini dati in modo interattivo.** Il programma di amministrazione può chiamare **SQLManageDataSources**, **SQLCreateDataSource**o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** visualizza una finestra di dialogo con cui l'utente può aggiungere, modificare o eliminare origini dati e specificare le opzioni di traccia; questa funzione viene chiamata quando la DLL del programma di installazione viene richiamata direttamente dal Pannello di controllo. **SQLCreateDataSource** visualizza una finestra di dialogo con cui l'utente può solo aggiungere origini dati. **SQLConfigDataSource** passa la chiamata direttamente alla DLL di installazione del driver.  
  
     In tutti i casi, la DLL del programma di installazione chiama **ConfigDSN** nella DLL di installazione del driver per aggiungere, modificare o eliminare effettivamente l'origine dati. La DLL di installazione del driver potrebbe richiedere all'utente ulteriori informazioni.  
  
-   **Aggiungere, modificare o eliminare origini dati in modo invisibile all'utente.** Il programma di amministrazione chiama **SQLConfigDataSource** nella DLL del programma di installazione e gli passa un handle di finestra null, il nome di un'origine dati da aggiungere, modificare o eliminare e un elenco di valori per il Registro di sistema. La DLL del programma di installazione chiama **ConfigDSN** nella DLL di installazione del driver per aggiungere, modificare o eliminare effettivamente l'origine dati.  
  
-   **Aggiungere, modificare o eliminare un'origine dati predefinita.** L'origine dati predefinita è uguale a qualsiasi altra origine dati, ad eccezione del fatto che il nome è Default.The default data source is the same as any other data source, except that it name is Default. Viene aggiunto, modificato o eliminato nello stesso modo di qualsiasi altra origine dati.
