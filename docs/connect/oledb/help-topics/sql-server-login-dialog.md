---
title: Finestra di dialogo account di accesso SQL Server (OLE DB) | Microsoft Docs
description: Uso della finestra di dialogo di accesso di SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 4735ead33dc7c3a6d633e3b23ff1da97eeae4962
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744873"
---
# <a name="sql-server-login-dialog-box"></a>Finestra di dialogo di accesso a SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Quando si prova a connettersi senza specificare informazioni sufficienti, il driver OLE DB consente di visualizzare il **account di accesso di SQL Server** nella finestra di dialogo.

> [!NOTE]  
> Il comportamento di richiesta della finestra di accesso di SQL Server viene controllata dal `DBPROP_INIT_PROMPT` proprietà di inizializzazione. Per altre informazioni, vedere:
> - [Proprietà di inizializzazione e di autorizzazione](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guida per programmatori OLE DB](https://go.microsoft.com/fwlink/?linkid=2067702)

![Screenshot della finestra di dialogo account di accesso SQL Server](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opzioni
|Opzione|Descrizione|
|---   |---        |
|Server|Il nome di un'istanza di SQL Server nella rete. Selezionare un nome di server o di istanza nell'elenco oppure digitarlo nella casella **Server**. Facoltativamente, è possibile creare un alias del server nel computer client tramite **Gestione configurazione SQL Server** e digitarlo nella casella **Server**. <br/><br/>È possibile immettere "(locale)" quando si usa lo stesso computer in cui è presente SQL Server. È quindi possibile connettersi a un'istanza locale di SQL Server anche in caso di esecuzione di una versione non in rete di SQL Server.<br/><br/>Per altre informazioni sui nomi dei server per i diversi tipi di reti, vedere [installazione di SQL Server](https://go.microsoft.com/fwlink/?linkid=2067541).|
|Modalità di autenticazione|Nell'elenco a discesa, è possibile selezionare le opzioni di autenticazione seguenti:<br/><ul><li>`Windows Authentication:` Autenticazione a SQL Server utilizzando le credenziali dell'account di Windows dell'utente connesso.</li><li>`SQL Server Authentication:` Autenticazione a SQL Server usando l'ID di accesso e la password.</li><li>`Active Directory - Integrated:` Autenticazione integrata con le credenziali dell'account di Windows dell'utente connesso.</li><li>`Active Directory - Password:` Autenticazione di Active Directory usando l'ID di accesso e la password.</li></ul>|
|SPN server|Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.|
|ID accesso|Specifica l'ID di accesso da utilizzare per la connessione. La casella di testo di un ID di accesso è abilitata solo se `Authentication Mode` è impostata su `SQL Server Authentication` o `Active Directory - Password`.|
|Password|Specifica la password utilizzata per la connessione. La casella di testo password è abilitata solo se `Authentication Mode` è impostata su `SQL Server Authentication` o `Active Directory - Password`.|
|Opzioni|Visualizza o nasconde il gruppo **Opzioni**. Il pulsante **Opzioni** è abilitato se per **Server** è specificato un valore.|
|Comando Cambia password|Quando viene selezionata, consente **nuova Password** e **Conferma nuova Password** caselle di testo.|
|Nuova password|Consente di specificare la nuova password.|
|Conferma nuova password|Consente di specificare la nuova password una seconda volta, per conferma.|
|Database|Selezionare o digitare il database predefinito da usare per la connessione. Questa impostazione è prioritaria rispetto al database predefinito specificato per l'accesso nel server. Se non è specificato alcun database, viene utilizzato il database predefinito specificato per l'account di accesso nel server.|
|Server mirror|Indica il nome del partner di failover del database da sottoporre a mirroring.|
|SPN mirror|Se si desidera, è possibile specificare un nome SPN per il server mirror. Tale nome verrà utilizzato per l'autenticazione reciproca tra client e server.|
|Linguaggio|Indica la lingua nazionale da usare per i messaggi di sistema di SQL Server. Tale lingua deve essere installata nel computer che esegue SQL Server. Questa impostazione è prioritaria rispetto alla lingua predefinita specificata per l'account di accesso nel server. Se non è specificata alcuna lingua, viene utilizzata la lingua predefinita specificata per l'account di accesso nel server.|
|Application Name|Indica il nome dell'applicazione da archiviare nella colonna **program_name**, in corrispondenza della riga relativa alla connessione corrente in **sys.sysprocesses**.|
|ID workstation|Indica l'ID della workstation da archiviare nella colonna **hostname** nella riga relativa alla connessione corrente in **sys.sysprocesses**.|
|Usa crittografia avanzata per i dati|Se selezionata, verranno crittografati i dati passati tramite la connessione.|
|Certificato server attendibile|Se selezionata, il certificato del server verrà convalidato. Certificato del server deve avere il nome host corretto del server e rilasciato da un'autorità di certificazione attendibile.|

> [!NOTE]  
> Quando si usa `Windows Authentication` oppure `SQL Server Authentication` modalità **considera attendibile certificato server** viene considerata solo quando il **Usa crittografia avanzata per i dati** opzione è abilitata.

## <a name="next-steps"></a>Passaggi successivi
- [Eseguire l'autenticazione ad Azure Active Directory](../features/using-azure-active-directory.md) usando il driver OLE DB.
- Informazioni di connessione set usando [Universal Data Link (UDL)](data-link-pages.md).