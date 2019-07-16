---
title: Appliance di installare e configurare - sistema di piattaforma Analitica | Microsoft Docs
description: Descrive gli amministratori di appliance Analitica piattaforma di strumenti analitici tramite i passaggi iniziali per configurare e iniziare a usare l'appliance di nuovo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1f32cbeccb9a71d1d4c801443b40df5a762b8f38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961485"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Installazione di Appliance e la configurazione per il sistema di piattaforma Analitica
Descrive gli amministratori di appliance Analitica piattaforma di strumenti analitici tramite i passaggi iniziali per configurare e iniziare a usare l'appliance di nuovo.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Installare i componenti Hardware  
L'appliance nuovo verrà recapitata su palette al dock presso il data center.  
  
> [!IMPORTANT]  
> In alcuni casi, fornitore IHV verrà Disimballare, installare in rack e collegare l'appliance automaticamente nel proprio data center. In caso affermativo, queste istruzioni non sono necessari e a cui è possibile ignorare il [3. Configurare l'Appliance](#ConfigureAppliance) sezione riportata di seguito.  
  
Se il fornitore non esegue l'installazione di hardware, usare la procedura seguente per installare i componenti hardware.  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Verificare la documentazione|Verificare di aver ricevuto tutte le informazioni e documenti necessari al fornitore di hardware indipendenti (IHV). Visualizzare [le informazioni per ottenere dal fornitore IHV &#40;sistema di piattaforma Analitica&#41;](information-to-obtain-from-your-ihv.md).|  
|Installazione hardware|Verificare che sia che il data center può gestire l'appliance. Spostare i componenti di dispositivo al data center. I commutatori di rete, PDU, installare in rack e cablaggio. Visualizzare [installazione Hardware &#40;sistema di piattaforma Analitica&#41;](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Accendere il dispositivo  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Accendere il dispositivo|Risparmio energia in ogni nodo del componente di appliance nell'ordine richiesto, in attesa in base alle esigenze per confermare che non si verificano errori.|  
  
## <a name="ConfigureAppliance"></a>3. Configurare l'Appliance  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|||  
|Configurare l'appliance usando SQL Server PDW**Configuration Manager**|Utilizzare Gestione configurazione per impostare le password di appliance, fusi orari, le impostazioni di rete e firewall, i certificati di sicurezza e le prestazioni e altre impostazioni nell'appliance. Visualizzare [la configurazione dell'Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> Modifiche di configurazione devono essere apportate soltanto usando SQL Server PDW**Configuration Manager**. Le modifiche non esposta attraverso **Configuration Manager** non sono supportati. Ad esempio, l'appliance di SQL Server PDW supporta solo l'impostazione della lingua inglese Stati Uniti.  
  
## <a name="SoftwareServicing"></a>4. Configurare Software di manutenzione  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Applicare gli aggiornamenti di SQL Server PDW|(Facoltativo) Potrebbe essere necessario applicare uno o più aggiornamenti di SQL Server PDW per aggiornare il software di SQL Server PDW per la versione più recente. Visualizzare [applicare le correzioni del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Configurare Windows Server Update Services|Configurare l'appliance per ricevere gli aggiornamenti da Windows Server Update Services per il supporto di software. Visualizzare [scaricare e applicare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Passaggi successivi  
Dopo aver completato tutti i passaggi precedenti, il dispositivo è pronto per l'uso. Si o altre persone nella posizione possono procedere con le attività seguenti.  
  
|||  
|-|-|  
|**Attività**|**Descrizione**|  
|Installare i driver di SQL Server PDW e configurare la connettività|Configurare i computer locali per connettersi a SQL Server PDW con SQL Server Data Tools, sqlcmd, software di business intelligence o altri strumenti. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Creare ruoli server e degli accessi e assegnare le autorizzazioni|Pianificare e creare ruoli server e gli accessi che consentiranno agli utenti di accedere a SQL Server PDW con le autorizzazioni appropriate. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurare il Gateway di gestione dati di Azure|Il Gateway consente agli utenti di Azure di accedere ai dati di punti di accesso locale all'esposizione dei dati di punti di accesso come proteggere i feed OData. Il Gateway è già installato nel nodo di controllo. Richiedere a Microsoft per assistenza con la configurazione.|  
|Le query di monitoraggio e gli utenti delle appliance|Usare la Console di amministrazione e altre risorse per monitorare le query e gli utenti di appliance. Visualizzare [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Caricare dati in SQL Server PDW|Caricare i dati nell'Appliance. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Creare un piano di ripristino di emergenza|Pianificare come si desidera proteggere i dati da errori hardware o lo sovrascrive i dati. Creare un piano tramite backup regolari e ripristinare i piani in caso di perdita o danneggiamento dei dati. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Monitorare l'appliance|Monitoraggio di stato dello strumento, l'integrità e delle prestazioni tramite le viste di sistema, log e la Console di amministrazione. Correggere o segnalare eventuali problemi. Visualizzare [lo stato di integrità di monitoraggio di Appliance &#40;sistema di piattaforma Analitica&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
