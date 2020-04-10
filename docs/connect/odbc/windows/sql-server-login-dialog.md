---
title: Finestra di dialogo Accesso a SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: 35a9c6b6c254d6ed7c3283aedba15e65b6114579
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920130"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Finestra di dialogo Account di accesso di SQL Server (ODBC)

Quando si chiama una connessione ODBC senza specificare informazioni sufficienti affinché il driver si connetta a SQL Server, il driver ODBC visualizza la finestra di dialogo **Accesso a SQL Server**.

## <a name="options"></a>Opzioni

### <a name="server"></a>Server

Nome di un'istanza di SQL Server in rete. Selezionare un nome di server o di istanza nell'elenco oppure digitarlo nella casella **Server**. Facoltativamente, è possibile creare un alias del server nel computer client tramite **Gestione configurazione SQL Server** e digitarlo nella casella **Server**.

È possibile immettere "(locale)" quando si usa lo stesso computer in cui è presente SQL Server. È quindi possibile connettersi a un'istanza locale di SQL Server anche in caso di esecuzione di una versione non in rete di SQL Server.

Per altre informazioni sui nomi dei server per tipi diversi di reti, vedere la documentazione relativa all'installazione di SQL Server nella documentazione online di SQL Server.

### <a name="authentication-mode"></a>Modalità di autenticazione

Selezionare una delle modalità di autenticazione seguenti:
- **SQL Server** con ID di accesso e password
- Autenticazione **integrata di Windows** con l'account dell'utente attualmente connesso
- **Password di Active Directory** con ID di accesso e password
- Autenticazione **integrata di Active Directory** con l'account dell'utente attualmente connesso
- **Autenticazione interattiva di Active Directory** con ID di accesso

Per altre informazioni sulle modalità di autenticazione, vedere la [schermata 2 della Creazione guidata origine dati](../../../connect/odbc/windows/dsn-wizard-2.md).

### <a name="server-spn"></a>SPN server

Se si utilizza una connessione trusted, è possibile specificare un nome dell'entità servizio (SPN) per il server.

### <a name="login-id"></a>ID accesso

Specifica l'ID di accesso di SQL Server o Azure Active Directory da usare per la connessione se **Modalità di autenticazione** è impostata su **SQL Server**, sulla **password di Active Directory** o sull'autenticazione **interattiva di Active Directory**. In caso contrario, la casella **ID di accesso** è disabilitata.

### <a name="password"></a>Password

Specifica la password per l'ID di accesso di SQL Server o Azure Active Directory usato per la connessione se **Modalità di autenticazione** è impostata su **SQL Server** o sulla **password di Active Directory**. In caso contrario, la casella **Password** è disabilitata.

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

### <a name="application-name"></a>Nome dell'applicazione

(Facoltativo) Indica il nome dell'applicazione da archiviare nella colonna **program_name**, in corrispondenza della riga relativa alla connessione corrente in **sys.sysprocesses**.

### <a name="workstation-id"></a>ID workstation

(Facoltativo) Indica l'ID della workstation da archiviare nella colonna **hostname** nella riga relativa alla connessione corrente in **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Usa crittografia avanzata per i dati

Se questa opzione è selezionata, i dati passati attraverso la connessione verranno crittografati. Gli account di accesso sono crittografati per impostazione predefinita, anche se questa casella di controllo è deselezionata.

### <a name="trust-server-certificate"></a>Certificato server attendibile

Questa opzione è applicabile solo quando è abilitata l'opzione **Usa crittografia avanzata per i dati**. Se questa opzione è selezionata, non viene verificato che il certificato del server abbia il nome host corretto del server e sia emesso da un'autorità di certificazione attendibile.

## <a name="see-also"></a>Vedere anche

[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
