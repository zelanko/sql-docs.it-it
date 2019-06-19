---
title: Configurare l'inizializzazione immediata dei File - sistema di piattaforma Analitica | Microsoft Docs
description: Configurare l'inizializzazione immediata dei File nel sistema di piattaforma Analitica. L'inizializzazione immediata dei file è una funzionalità di SQL Server che consente operazioni di file di dati eseguire più rapidamente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298126"
---
# <a name="instant-file-initialization-configuration"></a>Configurazione dell'inizializzazione immediata dei File
L'inizializzazione immediata dei file è una funzionalità di SQL Server che consente operazioni di file di dati eseguire più rapidamente. Selezionando la casella per attivare l'inizializzazione immediata dei File migliorerà le prestazioni di SQL Server PDW. Tuttavia, se ciò costituisce un rischio per la sicurezza per l'utente business, quindi lasciare deselezionata la casella.  
  
> [!IMPORTANT]  
> Quando è abilitata l'inizializzazione immediata dei file, SQL Server non vengono sovrascritte bits eliminato con zeri.  Questo comportamento è stato possibile creare una vulnerabilità di sicurezza se gli utenti non autorizzati ottengono l'accesso ai dati eliminati. Tuttavia, SQL Server PDW questo rischio si riduce, garantendo che il database di SQL Server e i file di backup sono sempre accodati a un'istanza di SQL Server. solo l'account del servizio SQL Server e amministratori locali possono accedere i dati eliminati in SQL Server PDW.  
  
L'inizializzazione immediata dei file non è disponibile quando è abilitata la crittografia TDE.  
  
## <a name="add-permission-for-the-backup-account"></a>Aggiungere l'autorizzazione per l'Account di Backup  
Il processo di backup richiede una credenziale di rete (account utente di Windows) che può accedere al percorso di archiviazione di backup. Si autorizza PDW per l'utilizzo di account usando il [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedure. Visualizzare [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md) per l'intero processo di backup. Per usare l'inizializzazione immediata dei file, l'account di backup deve essere concesse le `Perform volume maintenance tasks` l'autorizzazione.  
  
1.  Nel server di backup, aprire il **criteri di sicurezza locali** dell'applicazione (`secpol.msc`).  
  
2.  Nel riquadro sinistro espandere **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
3.  Nel riquadro destro fare doppio clic su **Esecuzione attività di manutenzione volume**.  
  
4.  Fare clic su **Aggiungi utente o gruppo** e aggiungere tutti gli account utente usati per i backup.  
  
5.  Fare clic su **Applica**, quindi chiudere tutte le finestre di dialogo di **Criteri di sicurezza locali** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Per attivare o disattivare la inizializzazione immediata dei File  
  
1.  Avviare Gestione configurazione. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro a sinistra di Configuration Manager, fare clic su **inizializzazione immediata dei File**.  
  
3.  Per abilitare l'inizializzazione immediata dei file, selezionare la casella accanto a **abilitare inizializzazione immediata dei File in tutti i nodi**. Per disattivare l'inizializzazione immediata dei file, deselezionare la casella accanto a **abilitare inizializzazione immediata dei File in tutti i nodi**.  
  
    > [!WARNING]  
    > Quando si disattiva l'inizializzazione immediata dei file, le considerazioni sulla protezione descritte sopra per la funzionalità verranno applicate ai file eliminati se è stata abilitata l'inizializzazione immediata dei file.  
  
4.  Fare clic su **Applica**. La modifica viene propagata attraverso le istanze di SQL Server in SQL Server PDW al successivo che riavvio dei servizi di appliance. Per riavviare i servizi di appliance ora, vedere [stato dei servizi PDW &#40;sistema di piattaforma Analitica&#41;](pdw-services-status.md).  
  
5.  È possibile ripetere i passaggi descritti in precedenza come **aggiungere l'autorizzazione per l'Account di Backup** per rimuovere il **eseguire le attività di manutenzione volume** l'autorizzazione.  
  
![DWConfig Appliance PDW Instant File Initialization](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Per altre informazioni sull'inizializzazione immediata dei file, vedere [inizializzazione immediata dei File](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  
