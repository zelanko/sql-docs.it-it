---
title: Inizializzazione immediata dei file di database | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41906481891908c85daf22c223e77826baa27766
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581986"
---
# <a name="database-file-initialization"></a>Inizializzazione di file di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
I file di dati e di log vengono inizializzati per sovrascrivere eventuali dati esistenti rimasti nel disco in seguito all'eliminazione precedente di file. I file di dati e di log vengono prima di tutto inizializzati azzerando i file (riempiendoli con zeri) quando si esegue una di queste operazioni:  
  
- Creazione di un database.  
- Aggiungere dati o file di log a un database esistente.  
- Aumento delle dimensioni di un file esistente (incluse operazioni di aumento automatico delle dimensioni).  
- Ripristino di un database o un filegroup.  
  
L'inizializzazione dei file richiede una quantità di tempo maggiore per l'esecuzione di tali operazioni. Quando i dati vengono scritti nei file per la prima volta, tuttavia, il sistema operativo non deve riempire i file con zeri.  
  
## <a name="instant-file-initialization-ifi"></a>Inizializzazione immediata dei file  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i file di dati possono essere inizializzati immediatamente per evitare operazioni di azzeramento. L'inizializzazione istantanea dei file consente l'esecuzione rapida delle operazioni sui file indicate in precedenza. Tramite l'inizializzazione dei file immediata infatti viene recuperato lo spazio su disco in uso evitando il riempimento di tale spazio con zeri. Il contenuto del disco viene invece sovrascritto via via che nuovi dati vengono scritti nei file. Per i file di log non è possibile eseguire l'inizializzazione immediata.  
  
> [!NOTE]
> L'inizializzazione immediata dei file è disponibile solo in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] o versioni successive.  
> 
> [!IMPORTANT]
> L'inizializzazione immediata dei file è disponibile solo per i file di dati. I file di log verranno sempre azzerati quando vengono creati o aumentano di dimensione.
  
L'inizializzazione immediata dei file è disponibile solo se all'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato concesso il diritto *SE_MANAGE_VOLUME_NAME*. I membri del gruppo Administrator di Windows dispongono di questo diritto e possono concederlo ad altri utenti aggiungendoli ai criteri di sicurezza **Esecuzione attività di manutenzione volume** .  
  
> [!IMPORTANT]
> L'uso di alcune funzionalità, ad esempio [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md), può impedire l'inizializzazione immediata dei file.  
  
Per concedere l'autorizzazione `Perform volume maintenance tasks` a un account:  
  
1.  Nel computer in cui verrà creato il file di dati aprire l'applicazione **Criteri di sicurezza locali** (`secpol.msc`).  
  
2.  Nel riquadro sinistro espandere **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
3.  Nel riquadro destro fare doppio clic su **Esecuzione attività di manutenzione volume**.  
  
4.  Fare clic su **Aggiungi utente o gruppo** e aggiungere l'account che esegue il servizio SQL Server.  
  
5.  Fare clic su **Applica**, quindi chiudere tutte le finestre di dialogo di **Criteri di sicurezza locali** .  

1. Riavviare il servizio SQL Server.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!NOTE]
> A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], è possibile concedere questa autorizzazione all'account del servizio al momento dell'installazione, durante la configurazione. Se si utilizza il [prompt dei comandi installare](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), aggiungere l'argomento /SQLSVCINSTANTFILEINIT o selezionare la casella *Grant Perform Volume Maintenance Task privilege to SQL Server Database Engine Service* (Concedi il privilegio di esecuzione attività di manutenzione volume al servizio motore di database di SQL Server) nell'[installazione guidata](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).

> [!NOTE]
> A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è possibile usare la colonna *instant_file_initialization_enabled* in [Sys.dm server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV per stabilire se è abilitata l'inizializzazione immediata dei file.

## <a name="remarks"></a>Remarks
Se all'[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]account di avvio del servizio viene concesso  *SE_MANAGE_VOLUME_NAME*, viene registrato un messaggio informativo simile al seguente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro errori all'avvio: 

`Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

Se all'[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]account di avvio del servizio **non** viene concesso *SE_MANAGE_VOLUME_NAME*, viene registrato un messaggio informativo simile al seguente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro errori all'avvio: 

`Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

**Si applica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>Considerazioni sulla sicurezza  
Se si utilizza l'inizializzazione immediata dei file, poiché il contenuto eliminato del disco viene sovrascritto solo quando vengono scritti nuovi dati nei file, il contenuto eliminato potrebbe essere accessibile a utenti o servizi non autorizzati, finché non vengono eseguite altre scritture dati in tale area specifica del file di dati. Finché il file di database è collegato all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questo rischio di diffusione di informazioni è ridotto dall'elenco di controllo di accesso discrezionale (DACL) per il file. Questo elenco consente l'accesso al file solo all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e all'amministratore locale. Quando il file viene scollegato, tuttavia, diventa accessibile a un utente o a un servizio privo del diritto *SE_MANAGE_VOLUME_NAME*. Una considerazione di questo tipo è necessaria quando viene eseguito un backup del database: se il file di backup non è protetto con un elenco di controllo di accesso discrezionale (DACL) appropriato, il contenuto eliminato può diventare disponibile a un utente o a un servizio non autorizzato.  

Tenere presente anche che quando un file usa l'inizializzazione immediata, un amministratore SQL Server può potenzialmente accedere ai contenuti delle pagine non elaborati e visualizzare i contenuti precedentemente eliminati.

Se i file di database sono ospitati in una rete di archiviazione, è anche possibile che la rete di archiviazione visualizzi sempre le pagine nuove come pagine preinizializzate e non sia necessario che il sistema operativo ne esegua nuovamente l'inizializzazione.
 
> [!NOTE]
> Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installato in un ambiente fisico sicuro, i vantaggi a livello di prestazioni ottenuti abilitando l'inizializzazione immediata dei file possono bilanciare il rischio per la sicurezza, il che spiega il motivo di questa raccomandazione.
  
Se la potenziale diffusione del contenuto eliminato rappresenta un problema, è consigliabile procedere con una o con entrambe le azioni seguenti:  
  
- Assicurarsi sempre che i file di dati e i file di backup scollegati presentino elenchi di controllo di accesso discrezionale (DACL) restrittivi.  
- Disabilitare l'inizializzazione immediata dei file per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revocando il diritto *SE_MANAGE_VOLUME_NAME* all'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!IMPORTANT]
> La disabilitazione dell'inizializzazione immediata dei file farà aumentare i tempi di allocazione per i file di dati.  
  
> [!NOTE]  
> La disabilitazione dell'inizializzazione immediata dei file ha effetto solo sui file che sono stati creati o le cui dimensioni sono aumentate dopo la revoca del diritto utente.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
