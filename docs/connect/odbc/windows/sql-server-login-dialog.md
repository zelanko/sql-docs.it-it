---
title: Finestra di dialogo SQL Server login (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
ms.openlocfilehash: fcfde122b978fa1e77baa690a1f3e09417dab1c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989417"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Finestra di dialogo Account di accesso di SQL Server (ODBC)

Quando si chiama una connessione ODBC senza specificare informazioni sufficienti affinché il driver si connetta a SQL Server, il driver ODBC visualizza la finestra di dialogo **Accesso a SQL Server**.

## <a name="options"></a>Opzioni

### <a name="server"></a>Server

Nome di un'istanza di SQL Server sulla rete. Selezionare un nome di server o di istanza nell'elenco oppure digitarlo nella casella **Server**. Facoltativamente, è possibile creare un alias del server nel computer client tramite **Gestione configurazione SQL Server** e digitarlo nella casella **Server**.

È possibile immettere "(locale)" quando si usa lo stesso computer in cui è presente SQL Server. È quindi possibile connettersi a un'istanza locale di SQL Server anche in caso di esecuzione di una versione non in rete di SQL Server.

Per altre informazioni sui nomi dei server per tipi diversi di reti, vedere la documentazione relativa all'installazione di SQL Server nella documentazione online di SQL Server.

### <a name="authentication-mode"></a>Modalità di autenticazione

Consente di selezionare la modalità di autenticazione da uno dei seguenti elementi:
- **SQL Server** con ID e password di accesso
- Autenticazione **integrata di Windows** con l'account dell'utente attualmente connesso
- **Active Directory password** con ID e password di accesso
- **Active Directory** l'autenticazione integrata con l'account dell'utente attualmente connesso
- **Autenticazione interattiva di Active Directory** con ID di accesso

Per ulteriori informazioni sulle modalità di autenticazione, vedere la [creazione guidata origine dati (schermata 2](../../../connect/odbc/windows/dsn-wizard-2.md) ).

### <a name="server-spn"></a>SPN server

Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.

### <a name="login-id"></a>ID accesso

Specifica il SQL Server o Azure Active Directory ID di accesso da utilizzare per la connessione se la **modalità di autenticazione** è impostata su **SQL Server** o **Active Directory password** o **Active Directory interattiva**. In caso contrario, la casella **ID di accesso** è disabilitata.

### <a name="password"></a>Password

Specifica la password per il SQL Server o Azure Active Directory ID di accesso utilizzato per la connessione se la **modalità di autenticazione** è impostata su **SQL Server** o **Active Directory password**. In caso contrario, la casella **password** è disabilitata.

### <a name="options"></a>Opzioni

Visualizza o nasconde il gruppo **Opzioni**. Il pulsante **Opzioni** è abilitato se per **Server** è specificato un valore.

### <a name="change-password"></a>Comando Cambia password

Quando questa casella è selezionata, vengono visualizzate le caselle **Nuova password** e **Conferma nuova password**.

### <a name="new-password"></a>Nuova password

Consente di specificare la nuova password.

### <a name="confirm-new-password"></a>Conferma nuova password

Consente di specificare la nuova password una seconda volta, per conferma.

### <a name="database"></a>Database

Indica il database predefinito da utilizzare per la connessione. Questa impostazione è prioritaria rispetto al database predefinito specificato per l'accesso nel server. Se non è specificato alcun database, viene utilizzato il database predefinito specificato per l'account di accesso nel server.

### <a name="mirror-server"></a>Server mirror

Indica il nome del partner di failover del database da sottoporre a mirroring.

### <a name="mirror-spn"></a>SPN mirror

Se si desidera, è possibile specificare un nome SPN per il server mirror. Tale nome verrà utilizzato per l'autenticazione reciproca tra client e server.

### <a name="language"></a>Linguaggio

Indica la lingua nazionale da usare per i messaggi di sistema di SQL Server. Tale lingua deve essere installata nel computer che esegue SQL Server. Questa impostazione è prioritaria rispetto alla lingua predefinita specificata per l'account di accesso nel server. Se non è specificata alcuna lingua, viene utilizzata la lingua predefinita specificata per l'account di accesso nel server.

### <a name="application-name"></a>Application Name

(Facoltativo) Indica il nome dell'applicazione da archiviare nella colonna **program_name**, in corrispondenza della riga relativa alla connessione corrente in **sys.sysprocesses**.

### <a name="workstation-id"></a>ID workstation

(Facoltativo) Indica l'ID della workstation da archiviare nella colonna **hostname** nella riga relativa alla connessione corrente in **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Usa crittografia avanzata per i dati

Quando questa opzione è selezionata, i dati passati attraverso la connessione verranno crittografati. Gli account di accesso sono crittografati per impostazione predefinita, anche se questa casella di controllo è deselezionata.

### <a name="trust-server-certificate"></a>Certificato server attendibile

Questa opzione è applicabile solo quando è abilitata l'opzione **Usa crittografia avanzata per i dati** . Quando questa opzione è selezionata, il certificato del server non viene convalidato in modo da avere il nome host corretto del server ed essere emesso da un'autorità di certificazione attendibile.

## <a name="see-also"></a>Vedere anche

[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
