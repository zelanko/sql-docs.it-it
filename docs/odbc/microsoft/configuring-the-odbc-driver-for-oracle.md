---
title: Configurazione del Driver ODBC per Oracle | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae444cfb293e12bd94281957335da1d4f4a97885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301745"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurazione del driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 È possibile controllare le prestazioni del Driver ODBC per Oracle di conoscere l'ambiente dei dati e correttamente impostando i parametri di connessione all'origine dati tramite il [Amministrazione origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md) dialogo casella o per la connessione parametri della stringa. La finestra di dialogo fornisce i seguenti controlli per la connessione a un'origine dati tramite la finestra di dialogo o usando stringhe di connessione:  
  
-   **Scheda DSN utente** Elenca i nomi delle origini dati locali nel computer.  
  
-   **Scheda DSN di sistema** consente di aggiungere o rimuovere un'origine dati di sistema. Origini dati di sistema sono accessibili da tutti gli utenti nel computer locale.  
  
-   **Nella scheda DSN su file** consente di aggiungere o rimuovere un'origine dati file dal computer locale. Origini dati dei file possono essere condiviso da tutti gli utenti autorizzati a installare il driver stesso.  
  
-   **Scheda driver** Elenca driver ODBC installati.  
  
-   **Scheda Tracing** consente di specificare la modalità gestione Driver ODBC tiene traccia di chiamate alle funzioni ODBC. È possibile configurare la traccia separatamente per ogni applicazione ODBC installati.  
  
-   **Scheda connessione Pooling** consente di selezionare le opzioni di connessione per ogni driver installato.  
  
-   **Informazioni sulla scheda** sono elencati i file dei componenti ODBC installati.  
  
 Dopo aver aggiunto un'origine dati, è possibile usare la **Amministrazione origine dati ODBC** finestra di dialogo per configurare l'accesso all'origine dati. Selezionare un'origine dati e quindi fare clic su una delle schede per modificare o esaminare le informazioni.
