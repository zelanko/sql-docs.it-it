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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305132"
---
# <a name="odbc-architecture"></a>Architettura ODBC
L'architettura ODBC prevede quattro componenti:  
  
-   **Applicazione** di Esegue l'elaborazione e chiama le funzioni ODBC per inviare istruzioni SQL e recuperare i risultati.  
  
-   **Gestione driver** Carica e Scarica i driver per conto di un'applicazione. Elabora le chiamate di funzione ODBC o le passa a un driver.  
  
-   **Driver** di Elabora le chiamate di funzione ODBC, invia richieste SQL a un'origine dati specifica e restituisce i risultati all'applicazione. Se necessario, il driver modifica la richiesta di un'applicazione in modo che la richiesta sia conforme alla sintassi supportata dal DBMS associato.  
  
-   **Origine dati** È costituito dai dati a cui l'utente vuole accedere e dal sistema operativo, DBMS e piattaforma di rete, se presenti, usati per accedere al sistema DBMS.  
  
 Si notino i punti seguenti sull'architettura ODBC. Per prima cosa possono esistere più driver e origini dati, che consentono all'applicazione di accedere simultaneamente ai dati da più origini dati. In secondo luogo, l'API ODBC viene utilizzata in due posizioni: tra l'applicazione e gestione driver e tra Gestione driver e ogni driver. L'interfaccia tra Gestione driver e i driver viene a volte definita *interfaccia del provider di servizi* o *SPI*. Per ODBC, il Application Programming Interface (API) e l'interfaccia del provider di servizi (SPI) sono gli stessi. ovvero Gestione driver e ogni driver hanno la stessa interfaccia per le stesse funzioni.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni](../../odbc/reference/applications.md)  
  
-   [Gestione driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Driver](../../odbc/reference/drivers.md)  
  
-   [Origini dati](../../odbc/reference/data-sources.md)
