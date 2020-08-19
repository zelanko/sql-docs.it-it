---
description: Configurazione del driver ODBC per Oracle
title: Configurazione del driver ODBC per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53bf5efc66ad260c0184baf95a254313319da5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483674"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurazione del driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 È possibile controllare le prestazioni del driver ODBC per Oracle conoscendo l'ambiente dei dati e impostando correttamente i parametri della connessione all'origine dati tramite la finestra di dialogo [Amministrazione origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md) o mediante parametri di stringa di connessione. Nella finestra di dialogo sono disponibili i controlli seguenti per la connessione a un'origine dati tramite la finestra di dialogo o l'utilizzo di stringhe di connessione:  
  
-   **Scheda DSN utente** Elenca i nomi delle origini dati locali per il computer.  
  
-   **Scheda DSN di sistema** Consente di aggiungere o rimuovere un'origine dati di sistema. È possibile accedere alle origini dati di sistema da tutti gli utenti nel computer locale.  
  
-   **Scheda DSN file** Consente di aggiungere o rimuovere un'origine dati file dal computer locale. Le origini dati dei file possono essere condivise da tutti gli utenti in cui è installato lo stesso driver.  
  
-   **Scheda driver** Elenca i driver ODBC installati.  
  
-   **Scheda traccia** Consente di specificare il modo in cui gestione driver ODBC traccia le chiamate alle funzioni ODBC. È possibile configurare la traccia separatamente per ogni applicazione ODBC installata.  
  
-   **Scheda pool di connessioni** Consente di selezionare le opzioni di connessione per ogni driver installato.  
  
-   **Scheda informazioni** Elenca i file dei componenti ODBC installati.  
  
 Dopo avere aggiunto un'origine dati, è possibile utilizzare la finestra di dialogo **Amministrazione origine dati ODBC** per configurare l'accesso all'origine dati. Selezionare un'origine dati, quindi fare clic su una delle schede per modificare o rivedere le informazioni.
