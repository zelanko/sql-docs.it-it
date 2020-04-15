---
title: Proprietà ODBC Architecture - Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305132"
---
# <a name="odbc-architecture"></a>Architettura ODBC
L'architettura ODBC è composta da quattro componenti:  
  
-   **Applicazione** Esegue l'elaborazione e chiama le funzioni ODBC per inviare istruzioni SQL e recuperare i risultati.  
  
-   **Gestione driver** Carica e scarica i driver per conto di un'applicazione. Elabora le chiamate di funzione ODBC o le passa a un driver.  
  
-   **Conducente** Elabora le chiamate di funzione ODBC, invia richieste SQL a un'origine dati specifica e restituisce i risultati all'applicazione. Se necessario, il driver modifica la richiesta di un'applicazione in modo che la richiesta sia conforme alla sintassi supportata dal DBMS associato.  
  
-   **Origine dati** Consiste nei dati a cui l'utente desidera accedere e dal sistema operativo associato, dal sistema DBMS e dalla piattaforma di rete (se presenti) utilizzati per accedere al DBMS.  
  
 Tenere presente i punti seguenti sull'architettura ODBC. In primo luogo, possono esistere più driver e origini dati, che consente all'applicazione di accedere contemporaneamente ai dati da più di un'origine dati. In secondo luogo, l'API ODBC viene utilizzata in due posizioni: tra l'applicazione e Gestione Driver e tra Gestione Driver e ogni driver. L'interfaccia tra Gestione Driver e i driver viene talvolta definita interfaccia del provider di *servizi* o *SPI*. Per ODBC, l'API (Application Programming Interface) e l'interfaccia del provider di servizi (SPI) sono uguali; vale a dire, Gestione Driver e ogni driver hanno la stessa interfaccia per le stesse funzioni.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni](../../odbc/reference/applications.md)  
  
-   [Gestione driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Driver](../../odbc/reference/drivers.md)  
  
-   [Origini dati](../../odbc/reference/data-sources.md)
