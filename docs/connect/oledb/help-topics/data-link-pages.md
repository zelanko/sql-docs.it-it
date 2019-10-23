---
title: Configurazione di Universal Data Link (UDL) | Microsoft Docs
description: Configurazione di Universal Data Link (UDL) con Microsoft OLE DB driver per SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d92555fba1d9e0a380ffdc9051817ddfae9ca4b7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381764"
---
# <a name="universal-data-link-udl-configuration"></a>Configurazione di UDL (Universal Data Link)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Scheda connessione
Utilizzare la scheda connessione per specificare la modalità di connessione ai dati mediante il driver Microsoft OLE DB per SQL Server.

![Screenshot delle pagine di data link OLE DB-scheda connessione](../media/data-link-pages-connection-tab.png)

Nella scheda Connessione, specifica del provider, vengono visualizzate solo le proprietà di connessione richieste da Microsoft OLE DB Driver for SQL Server.

|Opzione|Descrizione|
|---   |---        |
|Selezionare o immettere il nome di un server|Selezionare un nome di server dall'elenco a discesa oppure digitare il percorso del server in cui si trova il database a cui si desidera accedere. La selezione del database nel server è un'azione distinta. Aggiornare l'elenco facendo clic su "Aggiorna".
|Immettere le informazioni per l'accesso al server|Da questo elenco a discesa è possibile selezionare le opzioni di autenticazione seguenti: <ul><li>`Windows Authentication:` l'autenticazione per SQL Server utilizzando le credenziali dell'account di Windows dell'utente attualmente connesso.</li><li>`SQL Server Authentication:` l'autenticazione tramite ID e password di accesso.</li><li>`Active Directory - Integrated:` l'autenticazione integrata con un'identità Azure Active Directory. Questa modalità può essere usata anche per l'autenticazione di Windows per SQL Server.</li><li>`Active Directory - Password:` l'autenticazione con l'ID utente e la password con un'identità Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` l'autenticazione interattiva con un'identità Azure Active Directory. Questa modalità supporta Azure multi-factor authentication.</li></ul>|
|SPN server|Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.|
|Nome utente|Digitare l'ID utente da usare per l'autenticazione quando si accede all'origine dati.|
|Password|Digitare la password da usare per l'autenticazione quando si accede all'origine dati.|
|Nessuna password|Quando questa opzione è selezionata, consente al provider specificato di utilizzare una password vuota nella stringa di connessione.|
|Consenti salvataggio password|Quando questa opzione è selezionata, consente di salvare la password con la stringa di connessione. L'eventuale inclusione della password nella stringa di connessione dipende dalle funzionalità dell'applicazione chiamante. <br/><br/>**NOTA:** se salvata, la password viene restituita e salvata non mascherata e non crittografata.|
|Usa crittografia avanzata per i dati|Se questa opzione è selezionata, i dati passati attraverso la connessione verranno crittografati.|
|Certificato server attendibile|Se questa opzione è selezionata, il certificato del server verrà convalidato. Il certificato del server deve avere il nome host corretto del server e emesso da un'autorità di certificazione attendibile.|
|Selezione del database|Selezionare o digitare il nome del database a cui si vuole accedere.|
|Associa file di database con nome|Indica il nome del file primario di un database a cui è possibile collegarsi. Questo database viene associato e utilizzato come database predefinito per l'origine dati. Nella prima casella di testo, in questa sezione, digitare il nome del database da utilizzare per il file di database collegato.<br/><br/>Digitare il percorso completo del file di database da collegare nella casella di testo `Using the filename` oppure fare clic sul pulsante `...` per cercare il file di database.|
|Comando Cambia password|Visualizza la finestra di dialogo Cambia SQL Server password. |
|Test connessione|Fare clic per tentare una connessione all'origine dati specificata. Se la connessione non riesce, verificare che le impostazioni siano corrette. Ad esempio, è possibile che le connessioni non vengano eseguite correttamente se sono presenti errori ortografici o non viene rispettata la distinzione tra maiuscole e minuscole.|

## <a name="advanced-tab"></a>Avanzate - scheda
Utilizzare la scheda avanzate per visualizzare e impostare proprietà di inizializzazione aggiuntive.

![Screenshot delle pagine di data link OLE DB-scheda Avanzate](../media/data-link-pages-advanced-tab.png)

|Opzione|Descrizione|
|---   |---        |
| Connect timeout | Specifica la quantità di tempo (in secondi) per cui il driver Microsoft OLE DB per SQL Server attende il completamento dell'inizializzazione. Se l'inizializzazione scade, viene restituito un errore e la connessione non viene creata.|


> [!NOTE]  
>  Per informazioni più generali sulla connessione ai collegamenti dati, vedere [Panoramica dell'API di data link](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Passaggi successivi
- [Eseguire l'autenticazione a Azure Active Directory](../features/using-azure-active-directory.md) usando il driver OLE DB.

- [Richiedere all'utente le credenziali di autenticazione](../help-topics/sql-server-login-dialog.md) utilizzando il driver OLE DB.