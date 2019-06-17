---
title: Inizializzazione immediata dei file di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initializations [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 491c8a63c7ee3ed06c90356c58820f34ed3c0bf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872094"
---
# <a name="database-instant-file-initialization"></a>Inizializzazione immediata dei file di database
  I file di dati e di log vengono inizializzati per sovrascrivere eventuali dati esistenti rimasti nel disco in seguito all'eliminazione precedente di file. I file di dati e di log vengono innanzitutto inizializzati riempiendo i file con zeri quando si eseguono le operazioni seguenti:  
  
-   Creazione di un database.  
  
-   Aggiunta di file, log o dati a un database esistente.  
  
-   Aumento delle dimensioni di un file esistente (incluse operazioni di aumento automatico delle dimensioni).  
  
-   Ripristino di un database o un filegroup.  
  
 L'inizializzazione dei file richiede una quantità di tempo maggiore per l'esecuzione di tali operazioni. Quando i dati vengono scritti nei file per la prima volta, tuttavia, il sistema operativo non deve riempire i file con zeri.  
  
## <a name="instant-file-initialization"></a>Inizializzazione dei file immediata  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i file di dati possono essere inizializzati immediatamente. Questa caratteristica consente l'esecuzione rapida delle operazioni sui file indicate in precedenza. Tramite l'inizializzazione dei file immediata infatti viene recuperato lo spazio su disco in uso evitando il riempimento di tale spazio con zeri. Il contenuto del disco viene invece sovrascritto via via che nuovi dati vengono scritti nei file. Per i file di log non è possibile eseguire l'inizializzazione immediata.  
  
> [!NOTE]  
>  L'inizializzazione immediata dei file è disponibile solo in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] o versioni successive.  
  
 L'inizializzazione immediata dei file è disponibile solo se all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) è stato concesso il diritto SE_MANAGE_VOLUME_NAME. I membri del gruppo Administrator di Windows dispongono di questo diritto e possono concederlo ad altri utenti aggiungendoli ai criteri di sicurezza **Esecuzione attività di manutenzione volume** . Per altre informazioni sull'assegnazione di diritti utente, vedere la documentazione di Windows.  
  
 L'inizializzazione immediata dei file non è disponibile quando è abilitata la crittografia TDE.  
  
 Per concedere l'autorizzazione `Perform volume maintenance tasks` a un account:  
  
1.  Nel computer in cui verrà creato il file di backup, aprire l'applicazione `Local Security Policy` (`secpol.msc`).  
  
2.  Nel riquadro sinistro espandere **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
3.  Nel riquadro destro fare doppio clic su **Esecuzione attività di manutenzione volume**.  
  
4.  Fare clic su **Aggiungi utente o gruppo** e aggiungere tutti gli account utente usati per i backup.  
  
5.  Fare clic su **Apply**, quindi chiudere tutte `Local Security Policy` finestre di dialogo.  
  
### <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Poiché il contenuto eliminato del disco viene sovrascritto solo quando vengono scritti nuovi dati nei file, il contenuto eliminato potrebbe essere accessibile a utenti o servizi non autorizzati. Finché il file di database è collegato all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa minaccia di accesso alle informazioni è ridotta dall'elenco di controllo di accesso discrezionale (DACL) per il file. Questo elenco consente l'accesso al file solo all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e all'amministratore locale. Quando il file viene scollegato, tuttavia, diventa accessibile a un utente o a un servizio privo del diritto SE_MANAGE_VOLUME_NAME. Una minaccia analoga è presente quando si esegue il backup del database. Il contenuto eliminato può diventare disponibile a un utente o a un servizio non autorizzato se il file di backup non è protetto con un elenco di controllo di accesso discrezionale (DACL) appropriato.  
  
 Se la potenziale diffusione del contenuto eliminato rappresenta un problema, è consigliabile eseguire una o entrambe le operazioni seguenti:  
  
-   Assicurarsi sempre che i file di dati e i file di backup scollegati presentino elenchi di controllo di accesso discrezionale (DACL) restrittivi.  
  
-   Disabilitare l'inizializzazione immediata dei file per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revocando il diritto SE_MANAGE_VOLUME_NAME dall'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  La disabilitazione dell'inizializzazione immediata dei file ha effetto solo sui file che sono stati creati o le cui dimensioni sono aumentate dopo la revoca del diritto utente.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
