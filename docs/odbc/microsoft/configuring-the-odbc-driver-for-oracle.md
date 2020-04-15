---
title: Configurazione del driver ODBC per Oracle Documenti Microsoft
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
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281371"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurazione del driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 È possibile controllare le prestazioni del driver ODBC per Oracle conoscendo l'ambiente dati e impostando correttamente i parametri della connessione all'origine dati tramite la finestra di dialogo [Amministratore origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md) o i parametri della stringa di connessione. La finestra di dialogo fornisce i seguenti controlli per la connessione a un'origine dati tramite la finestra di dialogo o le stringhe di connessione:The dialog box provides the following controls for connecting to a data source using the dialog box or using connect strings:  
  
-   **Scheda DSN utente** Elenca i nomi delle origini dati locali al computer.  
  
-   **Scheda DSN di sistema** Consente di aggiungere o rimuovere un'origine dati di sistema. Le origini dati di sistema sono accessibili a tutti gli utenti del computer locale.  
  
-   **Scheda DSN su file** Consente di aggiungere o rimuovere un'origine dati file dal computer locale. Le origini dati su file possono essere condivise da tutti gli utenti che hanno installato lo stesso driver.  
  
-   **Scheda Driver** Elenca i driver ODBC installati.  
  
-   **Scheda Traccia** Consente di specificare il modo in cui Gestione Driver ODBC traccia le chiamate alle funzioni ODBC. È possibile configurare la traccia separatamente per ogni applicazione ODBC installata.  
  
-   **Scheda Pool di connessioni** Consente di selezionare le opzioni di connessione per ogni driver installato.  
  
-   **Scheda Informazioni** Elenca i file dei componenti ODBC installati.  
  
 Dopo aver aggiunto un'origine dati, è possibile utilizzare la finestra di dialogo **Amministratore origine dati ODBC** per configurare l'accesso all'origine dati. Selezionare un'origine dati e quindi fare clic su una delle schede per modificare o rivedere le informazioni.
