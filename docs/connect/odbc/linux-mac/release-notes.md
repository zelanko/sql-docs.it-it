---
title: Note sulla versione - Microsoft ODBC Driver for SQL Server in Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: d67b8bba1449cce473baa5313762c4933a72e250
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955862"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Note sulla versione per Microsoft ODBC Driver for SQL Server in Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS

**Nuove distribuzioni supportate**: 15 SuSE, Ubuntu 18.10, macOS 10.14

**Funzionalità aggiunte**:

- Azure Active Directory identità del servizio gestito (sistema e assegnata dall'utente) in modalità di autenticazione, per altre informazioni, vedere [usando Azure Active Directory con il Driver ODBC](../using-azure-active-directory.md)
- Possibilità di trasmettere i parametri di input in base alle colonne Always Encrypted, per altre informazioni, vedere [limitazioni del driver ODBC quando si usa Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)
- XA transazioni distribuite, per altre informazioni, vedere [utilizzando transazioni XA](../use-xa-with-dtc.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS

**Nuove distribuzioni supportate**: 18.04 Ubuntu

**Funzionalità aggiunte**:

Classificazione dei dati per Database SQL di Azure e SQL Server, per altre informazioni vedere [classificazione dei dati](../data-classification.md)

Supporta la codifica UTF-8 server

SQLBrowseConnect

Delle dipendenze dinamiche in `libcurl`:
- A partire da questa versione, la `libcurl` pacchetto non è presente una dipendenza esplicita. Il `libcurl` per OpenSSL o NSS è obbligatorio quando si usa l'autenticazione di Azure Key Vault o Azure Active Directory del pacchetto. Se si verifica un errore relative a `libcurl`, assicurarsi sia installato.

Inattività resilienza delle connessioni con parole chiave ConnectRetryCount e ConnectRetryInterval nella stringa di connessione (per altre informazioni, vedere [resilienza della connessione nel Driver ODBC Windows](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- Usare `SQL_COPT_SS_CONNECT_RETRY_COUNT`(sola lettura) per recuperare il numero di tentativi di connessione.
- Usare `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(sola lettura) per recuperare la lunghezza dell'intervallo di ripetizione dei tentativi di connessione.
- Connessione verrà ripetuta una volta per impostazione predefinita.


[Correzioni di bug](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS

**Funzionalità aggiunte**:

Supporto per `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` attributi di connessione (per altre informazioni, vedere [utilizzo di Always Encrypted con il Driver ODBC per SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Consente di controllare l'ora in cui è presente nella cache locale delle chiavi di crittografia di colonna, nonché lo scaricamento
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Consente all'applicazione limitare le operazioni di Always Encrypted per usare solo l'elenco specificato di chiavi Master della colonna



Supporto per il caricamento di `.rll` dal percorso predefinito (per altre informazioni, vedere [sezione "Caricamento File di risorse" nel documento di installazione](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Correzioni di bug](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS

**Nuove distribuzioni supportate**: macOS High Sierra e Ubuntu 17.10 

**Miglioramenti delle prestazioni**: maggiore di 10 volte il miglioramento delle prestazioni quando il driver converte da e verso UTF-8 o 16.

**Funzionalità aggiunte**:

Supporto per Always Encrypted per l'API BCP

Nuovo attributo di stringa di connessione UseFMTOnly fa sì che i driver per l'uso di metadati legacy in casi particolari che richiedono le tabelle temporanee.

Supporto per l'istanza gestita SQL di Azure (anteprima privata estesa). 
> [!NOTE]
> Esistono numerose differenze quando si usa l'istanza gestita:
> -   FILESTREAM non è supportato 
> -   Accesso del file System locale non è supportato, ma obbligatorio per elementi quali tracefiles 
> -   Crea tipo definito dall'utente da local path non è supportato 
> -   Non è supportata l'autenticazione integrata di Windows 
> -   DTC non è supportato 
> -   account 'sa' non è presente (l'account predefinito viene chiamato 'cloudSA')
> -   Errore di token TDS (0xAA) restituisce il nome server errato
> -   Non sono supportati i caratteri speciali nel nome del database 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] non è supportato
> -   I messaggi di errore vengono sempre visualizzati in inglese, indipendentemente dal linguaggio impostazioni (come Azure) 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS  

ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aggiunge il supporto per Always Encrypted e Azure Active Directory quando usato in combinazione con Microsoft SQL Server 2016.

**Nuove distribuzioni supportate**: OS X 10.11 e macOS 10.12: sono supportati nella prima versione del Driver ODBC in macOS. Ubuntu 16.10 è ora supportata anche, insieme a Red Hat 6, 7 e SUSE 12. Ogni piattaforma ha un pacchetto piattaforma pertinente (RPM o DEB) per semplificare l'installazione e configurazione.  Visualizzare [installazione del Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) per le istruzioni di installazione.

**modifiche apportate al supporto 2.3.1 di gestione Driver unixODBC**: driver ODBC non dipende più pacchetti personalizzati per la gestione driver unixODBC (tranne che su RedHat 6) e si basa su Gestione distribuzione del pacchetto per risolvere la dipendenza UnixODBC dal repository di distribuzione.

**Supporto per l'API BCP**: driver ODBC di Linux e macOS ora supporta l'uso del [le funzioni API BCP (**bcp_init**e così via.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>What ' s New in Microsoft ODBC Driver 13.0 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux  
Con Microsoft ODBC Driver 13.0 for SQL Server, SQL Server 2014 e SQL Server 2016 sono ora anche supportati.  

**Nuove distribuzioni supportate**:

Ubuntu è ora supportato, insieme a Red Hat e SUSE. Ogni piattaforma ha un pacchetto piattaforma pertinente (RPM o DEB) per semplificare l'installazione e configurazione.  Visualizzare [installazione del Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) per le istruzioni di installazione.

**Supporto 2.3.1 di gestione Driver unixODBC**: oltre a una Gestione driver più recente, è inoltre disponibile un pacchetto per l'installazione di questa dipendenza che semplifica l'installazione e configurazione.  

**Risoluzione dell'IP di rete trasparente**: risoluzione dell'IP di rete trasparente è una revisione della funzionalità di Failover su più Subnet esistente che interessa la sequenza di connessione del driver nel caso in cui il primo risolto IP del nome host non esiste rispondere e sono presenti più indirizzi IP associati al nome host.

**Supporto di TLS 1.2**: Microsoft ODBC Driver 13.0 for SQL Server in Linux supporta ora TLS 1.2 quando vengono usate le comunicazioni protette con SQL Server.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux  
Il driver ODBC in SUSE Linux (anteprima) supporta SUSE Linux Enterprise 11 Service Pack 2 a 64 bit. Per altre informazioni, vedere [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md).  

Il driver ODBC in Linux supporta [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Per altre informazioni, vedere [Driver ODBC in Linux il supporto per la disponibilità elevata, ripristino di emergenza](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

Il driver ODBC in Linux supporta le connessioni al database SQL di Microsoft Azure. Per altre informazioni, vedere la pagina relativa alla [procedura di connessione al database SQL di Windows Azure usando ODBC](https://msdn.microsoft.com/library/hh974312.aspx).  

Il `-l` opzione (timeout di accesso) è stato aggiunto a `bcp`. Per altre informazioni, vedere [Connessione a **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
