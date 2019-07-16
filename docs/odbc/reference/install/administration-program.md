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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9cb78dae32bb17598ee0e86c26e621be1b6362c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068559"
---
# <a name="administration-program"></a>Programma di amministrazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Un programma di amministrazione, l'amministratore ODBC, è incluso con il SDK di MDAC/SDK Windows. Questo programma e può essere ridistribuito dagli utenti di SDK. Inoltre, gli sviluppatori possono scrivere i propri programmi di amministrazione. In generale, gli sviluppatori di scrivono i propri programmi di amministrazione solo se desiderano mantenere controllo completo sulla configurazione dell'origine dati o se si siano configurando le origini dei dati direttamente da un'applicazione che funge da un programma di amministrazione. Ad esempio, un foglio di calcolo potrebbe consentire agli utenti di aggiungere e quindi usare le origini dati in fase di esecuzione.  
  
 Il programma di amministrazione carica innanzitutto il programma di installazione DLL. Chiama quindi le funzioni nel programma di installazione DLL per eseguire le attività seguenti:  
  
-   **Aggiungere, modificare o eliminare le origini dati in modo interattivo.** Il programma di amministrazione è possibile chiamare **SQLManageDataSources**, **SQLCreateDataSource**, o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** Visualizza una finestra di dialogo con cui l'utente può aggiungere, modificare o eliminare origini dati e specificare le opzioni di traccia; questa funzione viene chiamata quando il programma di installazione DLL viene richiamato direttamente dal Pannello di controllo. **SQLCreateDataSource** Visualizza una finestra di dialogo con cui l'utente può solo aggiungere origini dati. **SQLConfigDataSource** passa la chiamata direttamente per la DLL di installazione di driver.  
  
     In tutti i casi, chiama la DLL di installazione **ConfigDSN** nell'installazione del driver DLL per poter aggiungere, modificare o eliminare l'origine dati. La DLL di installazione di driver potrebbe richiedere all'utente informazioni aggiuntive.  
  
-   **Aggiungere, modificare o eliminare le origini dati in modo invisibile.** Il programma di amministrazione chiama **SQLConfigDataSource** nel programma di installazione di DLL e passate è una finestra nulla gestire, il nome di un'origine dati per aggiungere, modificare o eliminare e un elenco di valori per il Registro di sistema. Le chiamate DLL programma di installazione **ConfigDSN** nell'installazione del driver DLL per poter aggiungere, modificare o eliminare l'origine dati.  
  
-   **Aggiungere, modificare o eliminare un'origine dati predefinito.** L'origine dati predefinito è lo stesso come qualsiasi altra origine dati, ad eccezione del fatto che il suo nome è predefinito. Si è aggiunto, modificato o eliminato in modo identico a qualsiasi altra origine dati.
