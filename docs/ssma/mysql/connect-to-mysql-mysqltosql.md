---
title: Connect to MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7289b3d5b287c1619a08921eba5cc30ff741e3b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63252713"
---
# <a name="connect-to-mysql-mysqltosql"></a>Connettersi a MySQL (MySQLToSQL)
Usare la **connettersi a MySQL** finestra di dialogo per la connessione al database MySQL che si desidera eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **connettersi a MySQL**. Se si è già connessa, il comando viene **Riconnetti a MySQL**.  
  
## <a name="options"></a>Opzioni  
**Provider**  
  
Provider MySQL disponibile è MySQL 5.1 provider ODBC (attendibili).  
  
**Mode**  
  
La modalità predefinita è la modalità Standard. In modalità Standard immettere o selezionare i valori per il MySQL, nome del server, porta del server, nome utente e password.  
  
**Nome server**  
  
Immettere il nome del server MySQL. Questa è un'opzione di modalità Standard.  
  
**Porta server**  
  
Immettere la porta del Server. La porta del server predefinita è 3306. Questa è un'opzione di modalità Standard.  
  
**Nome utente**  
  
Immettere il nome utente che SSMA userà per connettersi al database MySQL.  
  
**Password**  
  
Immettere la password associata al nome utente.  
  
**SSL**  
  
Se si desidera connettersi in modo sicuro a MySQL, assicurarsi di usare di Secure Socket Layer (SSL), controllare la **SSL** casella di controllo.  
  
**Configurare**  
  
Fornisce un'opzione per configurare la connessione a MySQL tramite Secure Socket Layer (SSL).  
  
> [!NOTE]  
> Per abilitare **Configure**, SSL deve essere impostata su **True**.  
  
Facendo clic sul pulsante "Configura", viene visualizzata una finestra di dialogo. Utilizzare la crittografia durante la connessione al MySQL Database, percorso file tre certificato seguenti presente nella finestra di dialogo deve essere definito [Privacy avanzata posta certificati (PEM)]:  
  
-   **Autorità di certificazione SSL:** Specifica il percorso di un file con un elenco di attendibilità SSL CA.  
  
-   **Certificato SSL:** Specifica il nome del file del certificato SSL da utilizzare per stabilire una connessione sicura.  
  
-   **CHIAVE SSL:** Specifica il nome del file di chiave SSL da utilizzare per stabilire una connessione sicura.  
  
> [!NOTE]  
> -   Il **OK** pulsante viene abilitato quando sono state fornite le informazioni necessarie. Se sono presenti i percorsi dei file non validi, il pulsante "OK" rimarrà disabilitato.  
> -   Il **annullare** pulsante chiude la finestra di dialogo e **disattiva** l'opzione SSL dal Form di connessione principale.  
  
