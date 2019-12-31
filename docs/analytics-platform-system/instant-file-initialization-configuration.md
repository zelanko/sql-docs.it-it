---
title: Configura inizializzazione immediata file
description: Configurare l'inizializzazione immediata del file nel sistema di piattaforma di analisi. L'inizializzazione immediata dei file è una funzionalità SQL Server che consente l'esecuzione più rapida delle operazioni sui file di dati.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 83ed373fd4fdd38ae5ddd391678b74e3d2e168c9
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401109"
---
# <a name="instant-file-initialization-configuration"></a>Configurazione inizializzazione file immediata
L'inizializzazione immediata dei file è una funzionalità SQL Server che consente l'esecuzione più rapida delle operazioni sui file di dati. Se si seleziona la casella per attivare l'inizializzazione immediata dei file, le prestazioni di SQL Server PDW migliorano. Tuttavia, se ciò costituisce un rischio per la sicurezza per l'azienda, lasciare la casella deselezionata.  
  
> [!IMPORTANT]  
> Quando l'inizializzazione immediata dei file è abilitata, SQL Server non sovrascrive i bit eliminati con zeri.  Questo comportamento potrebbe creare una vulnerabilità di sicurezza se utenti non autorizzati ottengono l'accesso ai dati eliminati. Tuttavia, SQL Server PDW attenua questo rischio garantendo che il database di SQL Server e i file di backup siano sempre collegati a un'istanza di SQL Server; solo l'account del servizio SQL Server e l'amministratore locale possono accedere ai dati eliminati SQL Server PDW.  
  
L'inizializzazione immediata dei file non è disponibile quando è abilitata la crittografia TDE.  
  
## <a name="add-permission-for-the-backup-account"></a>Aggiungere l'autorizzazione per l'account di backup  
Il processo di backup richiede una credenziale di rete (account utente di Windows) che può accedere al percorso di archiviazione di backup. Per autorizzare PDW a usare l'account, usare la procedura [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) . Vedere [backup database](../t-sql/statements/backup-database-parallel-data-warehouse.md) per l'intero processo di backup. Per usare l'inizializzazione immediata dei file, all'account di backup `Perform volume maintenance tasks` deve essere concessa l'autorizzazione.  
  
1.  Nel server di backup aprire l'applicazione **criteri di sicurezza locali** (`secpol.msc`).  
  
2.  Nel riquadro sinistro espandere **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
3.  Nel riquadro destro fare doppio clic su **Esecuzione attività di manutenzione volume**.  
  
4.  Fare clic su **Aggiungi utente o gruppo** e aggiungere tutti gli account utente usati per i backup.  
  
5.  Fare clic su **Applica**, quindi chiudere tutte le finestre di dialogo di **Criteri di sicurezza locali** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Per attivare o disattivare l'inizializzazione immediata di file  
  
1.  Avviare il Configuration Manager. Per ulteriori informazioni, vedere [la pagina relativa all'avvio del&#41;di sistema della piattaforma Configuration Manager &#40;Analytics ](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della Configuration Manager fare clic su **inizializzazione immediata dei file**.  
  
3.  Per attivare l'inizializzazione immediata dei file, selezionare la casella accanto a **Abilita inizializzazione immediata dei file in tutti i nodi**. Per disattivare l'inizializzazione immediata dei file, deselezionare la casella accanto a **Abilita inizializzazione immediata dei file su tutti i nodi**.  
  
    > [!WARNING]  
    > Quando si disattiva l'inizializzazione immediata dei file, è possibile che la considerazione di sicurezza descritta sopra per la funzionalità sia ancora applicabile ai file eliminati mentre è stata abilitata l'inizializzazione immediata dei file.  
  
4.  Fare clic su **Applica** La modifica verrà propagata attraverso le istanze di SQL Server in SQL Server PDW alla successiva riavvio dei servizi Appliance. Per riavviare ora i servizi Appliance, vedere [lo stato dei servizi PDW &#40;&#41;di sistema della piattaforma di analisi ](pdw-services-status.md).  
  
5.  Potrebbe essere necessario ripetere i passaggi descritti in precedenza come **Aggiungi autorizzazione per l'account di backup** per rimuovere l'autorizzazione **Esegui attività di manutenzione volume** .  
  
![Inizializzazione file immediata PDW strumento DWConfig](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Per ulteriori informazioni sull'inizializzazione immediata dei file, vedere [inizializzazione immediata dei file](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  
