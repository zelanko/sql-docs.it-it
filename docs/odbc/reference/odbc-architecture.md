---
title: Architettura ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 781a214d3ca059a442680c332d79aad48914976c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111226"
---
# <a name="odbc-architecture"></a>Architettura ODBC
L'architettura ODBC include quattro componenti:  
  
-   **Applicazione** esegue l'elaborazione e chiamate di funzioni ODBC per inviare istruzioni SQL e recuperare i risultati.  
  
-   **Gestione driver** carica e scarica i driver per conto di un'applicazione. Funzione ODBC processi chiama o li passa a un driver.  
  
-   **Driver** funzione processi ODBC chiama, invia le richieste SQL a un'origine dati specifica e restituisce i risultati all'applicazione. Se necessario, il driver modifica richiesta di un'applicazione in modo che la richiesta è conforme alla sintassi supportata dal sistema DBMS associato.  
  
-   **Zdroj dat** Consists dei dati l'utente desidera accedere e il sistema operativo associato, DBMS e piattaforma di rete (se presente) utilizzato per accedere a DBMS.  
  
 Tenere presente quanto segue sull'architettura di ODBC. Possono esistere prima, più i driver e origini dati, che consente all'applicazione di accedere simultaneamente ai dati da più di un'origine dati. In secondo luogo, l'API ODBC viene utilizzato in due posizioni: tra l'applicazione e la gestione di Driver e tra gestione Driver e ogni driver. L'interfaccia tra gestione Driver e i driver è talvolta detta il *interfaccia di service provider interface* o *SPI*. Per ODBC, l'application programming interface (API) e l'interfaccia di provider di servizi (SPI) sono uguali. vale a dire, la gestione di Driver e ogni driver hanno la stessa interfaccia per le stesse funzioni.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni](../../odbc/reference/applications.md)  
  
-   [Gestione driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Driver](../../odbc/reference/drivers.md)  
  
-   [Origini dati](../../odbc/reference/data-sources.md)
