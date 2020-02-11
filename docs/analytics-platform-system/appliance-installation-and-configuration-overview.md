---
title: Installazione e configurazione dell'appliance
description: Consente di esplorare gli amministratori di appliance del sistema di piattaforma di analisi (APS) seguendo i passaggi iniziali per configurare e iniziare a usare il nuovo Appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9f96d953dbd427bfb6cf94470c0ee80ade3aed48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401441"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Installazione e configurazione di appliance per il sistema della piattaforma Analytics
Consente di esplorare gli amministratori di appliance del sistema di piattaforma di analisi (APS) seguendo i passaggi iniziali per configurare e iniziare a usare il nuovo Appliance.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. installare l'hardware  
Il nuovo appliance verrà distribuito sui pallet al Dock nel data center.  
  
> [!IMPORTANT]  
> In alcuni casi, il IHV decomprimere, eseguire il rack e connettere il dispositivo all'utente nel data center. In tal caso, queste istruzioni non sono necessarie ed è possibile passare a [3. Configurare la sezione Appliance riportata di](#ConfigureAppliance) seguito.  
  
Se il IHV non esegue l'installazione dell'hardware, attenersi alla procedura seguente per installare l'hardware.  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Conferma documentazione|Verificare di aver ricevuto tutte le informazioni e i documenti necessari dal fornitore dell'hardware indipendente (IHV). Vedere [le informazioni da ottenere dalla piattaforma IHV &#40;Analytics System&#41;](information-to-obtain-from-your-ihv.md).|  
|Installare l'hardware|Verificare che l'data center possa contenere l'appliance. Spostare i componenti dell'appliance nel data center. Rack i commutatori di rete, PDU e cablaggio. Vedere [Installazione Hardware &#40;&#41;di sistema della piattaforma di analisi ](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Accendere l'appliance  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Accendere l'appliance|Accendere ogni nodo del componente Appliance nell'ordine necessario, in attesa di verificare che non vengano rilevati errori.|  
  
## <a name="ConfigureAppliance"></a>3. configurare l'appliance  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|||  
|Configurare l'appliance usando il SQL Server PDW**Configuration Manager**|Usare il Configuration Manager per impostare le password dell'appliance, i fusi orari, le impostazioni di rete e del firewall, i certificati di sicurezza e le prestazioni e altre impostazioni nel dispositivo. Vedere [configurazione del dispositivo &#40;&#41;di sistema della piattaforma di analisi ](appliance-configuration.md).|  
  
> [!WARNING]  
> Le modifiche alla configurazione devono essere apportate solo usando il SQL Server PDW**Configuration Manager**. Le modifiche non esposte tramite **Configuration Manager** non sono supportate. Ad esempio, l'appliance SQL Server PDW supporta solo l'impostazione della lingua inglese (Stati Uniti).  
  
## <a name="SoftwareServicing"></a>4. configurare la manutenzione del software  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Applicare gli aggiornamenti di SQL Server PDW|Opzionale Potrebbe essere necessario applicare uno o più aggiornamenti SQL Server PDW per aggiornare il software SQL Server PDW alla versione più recente. Vedere applicare gli hotfix del sistema della piattaforma di [analisi &#40;&#41;del sistema della piattaforma di analisi ](apply-analytics-platform-system-hotfixes.md).|  
|Configurare Windows Server Update Services|Configurare l'appliance per la ricezione di aggiornamenti da Windows Server Update Services per il software di supporto. Vedere [scaricare e applicare gli aggiornamenti Microsoft &#40;&#41;di sistema della piattaforma di analisi ](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Passaggi successivi  
Dopo aver completato tutti i passaggi precedenti, l'appliance è pronta per l'uso. L'utente o altri addetti alla propria sede possono procedere con le attività seguenti.  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Installare i driver SQL Server PDW e configurare la connettività|Configurare i computer locali per la connessione a SQL Server PDW tramite SQL Server Data Tools, sqlcmd, business intelligence software o altri strumenti. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Creare accessi e ruoli del server e assegnare autorizzazioni|Pianificare e creare accessi e ruoli del server che consentiranno agli utenti di accedere a SQL Server PDW con le autorizzazioni appropriate. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurare il gateway di Azure Gestione dati|Il gateway consente agli utenti di Azure di accedere ai dati APS locali esponendo i dati APS come feed OData protetti. Il gateway è già installato nel nodo di controllo. Chiedere assistenza a Microsoft per la configurazione.|  
|Monitorare le query e gli utenti degli appliance|Usare la console di amministrazione e altre risorse per monitorare le query e gli utenti dell'appliance. Vedere [monitorare l'appliance usando la console di amministrazione &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Caricare i dati in SQL Server PDW|Caricare i dati nell'appliance. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Creare un piano di ripristino di emergenza|Pianificare la modalità di protezione dei dati da errori hardware o da sovrascrittura dei dati. Creare un piano usando backup regolari e piani di ripristino in caso di danneggiamento o perdita di dati. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Monitorare l'appliance|Monitorare lo stato, l'integrità e le prestazioni dell'appliance usando le viste di sistema, i log e la console di amministrazione. Correggere o segnalare eventuali problemi. Vedere [monitorare lo stato di integrità dell'Appliance &#40;&#41;del sistema della piattaforma di analisi ](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
