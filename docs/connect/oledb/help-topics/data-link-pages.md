---
title: Universal Data Link (UDL) configurazione | Microsoft Docs
description: Configurazione di Data Link (UDL) universale mediante il Driver OLE DB Microsoft per SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744817"
---
# <a name="universal-data-link-udl-configuration"></a>Configurazione di Universal Data Link (UDL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Scheda connessione
Utilizzare la scheda connessione per specificare come connettersi ai dati tramite il Driver OLE DB Microsoft per SQL Server.

![Schermata di OLE DB collegamento delle pagine di dati - scheda connessione](../media/data-link-pages-connection-tab.png)

Nella scheda Connessione, specifica del provider, vengono visualizzate solo le proprietà di connessione richieste da Microsoft OLE DB Driver for SQL Server.

|Opzione|Descrizione|
|---   |---        |
|Selezionare o immettere il nome di un server|Selezionare un nome di server dall'elenco a discesa oppure digitare il percorso del server in cui si trova il database a cui si desidera accedere. La selezione del database nel server è un'azione distinta. Aggiornare l'elenco facendo clic su "Aggiorna".
|Immettere le informazioni per accedere al server|È possibile selezionare le seguenti opzioni di autenticazione da questo elenco a discesa: <ul><li>`Windows Authentication:` Autenticazione a SQL Server utilizzando le credenziali dell'account di Windows dell'utente connesso.</li><li>`SQL Server Authentication:` Autenticazione a SQL Server usando l'ID di accesso e la password.</li><li>`Active Directory - Integrated:` Autenticazione integrata con le credenziali dell'account di Windows dell'utente connesso.</li><li>`Active Directory - Password:` Autenticazione di Active Directory usando l'ID di accesso e la password.</li></ul>|
|SPN server|Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.|
|Nome utente|Digitare l'ID utente da utilizzare per l'autenticazione quando si accede all'origine dati.|
|Password|Digitare la password da utilizzare per l'autenticazione quando si accede all'origine dati.|
|Nessuna password|Se selezionata, consente al provider specificato di usare una password vuota nella stringa di connessione.|
|Consenti salvataggio password|Se selezionata, consente la password deve essere salvato con la stringa di connessione. L'eventuale inclusione della password nella stringa di connessione dipende dalle funzionalità dell'applicazione chiamante. <br/><br/>**NOTA:** se salvata, la password viene restituita e salvata non mascherata e non crittografata.|
|Usa crittografia avanzata per i dati|Se selezionata, verranno crittografati i dati passati tramite la connessione.|
|Certificato server attendibile|Se selezionata, il certificato del server verrà convalidato. Certificato del server deve avere il nome host corretto del server e rilasciato da un'autorità di certificazione attendibile.|
|Selezione del database|Selezionare o digitare il nome del database che si desidera accedere.|
|Associa file di database con nome|Indica il nome del file primario di un database a cui è possibile collegarsi. Questo database viene associato e utilizzato come database predefinito per l'origine dati. Nella prima casella di testo in questa sezione, digitare il nome del database da utilizzare per il file di database collegato.<br/><br/>Digitare il percorso completo al file di database da collegare nella casella di testo etichettato `Using the filename`, oppure fare clic su di `...` per cercare il file di database.|
|Comando Cambia password|Visualizza finestra di dialogo Modifica Password SQL Server. |
|Test connessione|Fare clic per tentare una connessione all'origine dati specificata. Se la connessione non riesce, verificare che le impostazioni siano corrette. Ad esempio, è possibile che le connessioni non vengano eseguite correttamente se sono presenti errori ortografici o non viene rispettata la distinzione tra maiuscole e minuscole.|

## <a name="advanced-tab"></a>Avanzate - scheda
Utilizzare la scheda Avanzate per visualizzare e impostare le proprietà di inizializzazione aggiuntiva.

![Schermata di OLE DB collegamento delle pagine di dati - scheda Avanzate](../media/data-link-pages-advanced-tab.png)

|Opzione|Descrizione|
|---   |---        |
| Connect timeout | Specifica la quantità di tempo (in secondi) che il Driver OLE DB Microsoft per SQL Server è in attesa del completamento dell'inizializzazione. Se l'inizializzazione scade, viene restituito un errore e la connessione non viene creata.|


> [!NOTE]  
>  Per informazioni di connessione di collegamento dati più generali, vedere la [Introduzione all'API di collegamento dati](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Passaggi successivi
- [Eseguire l'autenticazione ad Azure Active Directory](../features/using-azure-active-directory.md) usando il driver OLE DB.

- [Richiedere all'utente le credenziali di autenticazione](../help-topics/sql-server-login-dialog.md) usando il driver OLE DB.