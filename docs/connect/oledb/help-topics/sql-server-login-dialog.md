---
title: Finestra di dialogo Accesso a SQL Server (OLE DB) | Microsoft Docs
description: Uso della finestra di dialogo di accesso di SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d35c339798b4385cb903d8a4a83f13184bbf4db3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381749"
---
# <a name="sql-server-login-dialog-box"></a>Finestra di dialogo di accesso a SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Quando si tenta di connettersi senza specificare informazioni sufficienti, il driver OLE DB visualizza la finestra di dialogo **Accesso a SQL Server**.

> [!NOTE]  
> Il comportamento di richiesta della finestra di dialogo Accesso a SQL Server è controllato dalla proprietà di inizializzazione `DBPROP_INIT_PROMPT`. Per altre informazioni, vedere:
> - [Proprietà di inizializzazione e di autorizzazione](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guida per i programmatori OLE DB](https://go.microsoft.com/fwlink/?linkid=2067702)

![Screenshot della finestra di dialogo Accesso a SQL Server](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opzioni
|Opzione|Descrizione|
|---   |---        |
|Server|Nome di un'istanza di SQL Server in rete. Selezionare un nome di server o di istanza nell'elenco oppure digitarlo nella casella **Server**. Facoltativamente, è possibile creare un alias del server nel computer client tramite **Gestione configurazione SQL Server** e digitarlo nella casella **Server**. <br/><br/>È possibile immettere "(locale)" quando si usa lo stesso computer in cui è presente SQL Server. È quindi possibile connettersi a un'istanza locale di SQL Server anche in caso di esecuzione di una versione non in rete di SQL Server.<br/><br/>Per altre informazioni sui nomi dei server per i diversi tipi di rete, vedere [Installazione di SQL Server](https://go.microsoft.com/fwlink/?linkid=2067541).|
|Modalità di autenticazione|Dall'elenco a discesa è possibile selezionare le opzioni di autenticazione seguenti:<br/><ul><li>`Windows Authentication:` Autenticazione per SQL Server con le credenziali dell'account di Windows dell'utente attualmente connesso.</li><li>`SQL Server Authentication:` Autenticazione con ID di accesso e password.</li><li>`Active Directory - Integrated:` Autenticazione integrata con un'identità di Azure Active Directory. Questa modalità può essere usata anche per l'autenticazione di Windows per SQL Server.</li><li>`Active Directory - Password:`Autenticazione di ID utente e password con un'identità di Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` Autenticazione interattiva con un'identità di Azure Active Directory. Questa modalità supporta l'autenticazione a più fattori (MFA) di Azure.</li></ul>|
|SPN server|Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.|
|ID accesso|Immettere l'ID di accesso da usare per la connessione. La casella di testo ID accesso è abilitata solo se `Authentication Mode` è impostata su `SQL Server Authentication`, `Active Directory - Password` o `Active Directory - Universal with MFA support`.|
|Password|Specifica la password usata per la connessione. La casella di testo della password è abilitata solo se `Authentication Mode` è impostata su `SQL Server Authentication` o `Active Directory - Password`.|
|Opzioni|Visualizza o nasconde il gruppo **Opzioni**. Il pulsante **Opzioni** è abilitato se per **Server** è specificato un valore.|
|Comando Cambia password|Quando questa opzione è selezionata, abilita le caselle di testo **Nuova password** e **Conferma nuova password**.|
|Nuova password|Consente di specificare la nuova password.|
|Conferma nuova password|Consente di specificare la nuova password una seconda volta, per conferma.|
|Database|Selezionare o digitare il database predefinito da usare per la connessione. Questa impostazione è prioritaria rispetto al database predefinito specificato per l'accesso nel server. Se non è specificato alcun database, viene utilizzato il database predefinito specificato per l'account di accesso nel server.|
|Server mirror|Indica il nome del partner di failover del database da sottoporre a mirroring.|
|SPN mirror|Se si desidera, è possibile specificare un nome SPN per il server mirror. Tale nome verrà utilizzato per l'autenticazione reciproca tra client e server.|
|Linguaggio|Indica la lingua nazionale da usare per i messaggi di sistema di SQL Server. Tale lingua deve essere installata nel computer che esegue SQL Server. Questa impostazione è prioritaria rispetto alla lingua predefinita specificata per l'account di accesso nel server. Se non è specificata alcuna lingua, viene utilizzata la lingua predefinita specificata per l'account di accesso nel server.|
|Nome dell'applicazione|Indica il nome dell'applicazione da archiviare nella colonna **program_name**, in corrispondenza della riga relativa alla connessione corrente in **sys.sysprocesses**.|
|ID workstation|Indica l'ID della workstation da archiviare nella colonna **hostname** nella riga relativa alla connessione corrente in **sys.sysprocesses**.|
|Usa crittografia avanzata per i dati|Se questa opzione è selezionata, i dati passati attraverso la connessione verranno crittografati.|
|Certificato server attendibile|Se questa opzione è selezionata, il certificato del server verrà convalidato. Il certificato del server deve avere il nome host corretto del server e deve essere emesso da un'autorità di certificazione attendibile.|

> [!NOTE]  
> Quando si usano le modalità `Windows Authentication` o `SQL Server Authentication`, l'opzione **Considera attendibile il certificato del server** viene considerata solo quando è abilitata l'opzione **Usa crittografia avanzata per i dati**.

## <a name="next-steps"></a>Passaggi successivi
- [Eseguire l'autenticazione per Azure Active Directory](../features/using-azure-active-directory.md) usando il driver OLE DB.
- Impostare le informazioni di connessione usando [Universal Data Link (UDL)](data-link-pages.md).