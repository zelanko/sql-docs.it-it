---
title: Configurazione del firewall PDW - sistema di piattaforma Analitica | Microsoft Docs
description: La pagina firewall di Gestione configurazione SQL Server PDW consente di abilitare o disabilitare le regole del firewall che consentono o impediscono l'accesso a determinate porte nell'appliance di sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6f650aac34e3a5299cabae500a8ee73250c3974d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960415"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configurazione del firewall Parallel Data Warehouse nel sistema di piattaforma Analitica

Il **Firewall** pagina di Gestione configurazione SQL Server PDW consente di abilitare o disabilitare le regole del firewall che consentono o impediscono l'accesso a determinate porte nell'appliance di sistema di piattaforma Analitica.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Per gestire le porte e regole per i nodi di appliance firewall  
  
1.  Avviare Gestione configurazione. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro a sinistra di Configuration Manager, espandere **Parallel Data Warehouse topologia**, quindi fare clic su **Firewall**.  
  
3.  Trovare la regola di porta o un firewall per aggiornamento nell'elenco di configurazione e quindi selezionare o deselezionare la casella accanto a tale elemento. In questo elenco, incluse l'apertura e chiusura di porte con connessione esterna nodi vengono visualizzate solo opzioni configurabili dall'amministratore di SQL Server PDW.  
  
4.  Fare clic su **applica** per salvare le modifiche.  
  
![Firewall PDW Appliance DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Le porte esterne  
Le porte seguenti siano aperte per le connessioni client provenienti all'esterno di PDW.  
  
|Scopo|N. porta|Nodi|  
|-----------|-----------|---------|  
|Accesso di SQL Client per PDW (TDS)|17001|CTL|  
|Accesso Client del caricatore (dwloader & SSIS)|8001|CTL|  
|Accesso desktop remoto|3389|ELENCO DI SCOPI CONSENTITI, CMP|  
|BinaryLoaderDataChannel SSIS|16551|CTL|  
|BinaryLoaderDataChannel dwloader|16551|CMP|  
|SSL crittografata connessioni (per le comunicazioni interne, per accedere alla Console di amministrazione)|443|Tutti i nodi|  
|SQL Server PDW carico controllo flusso - le credenziali di Windows|8002|CTL|  
|_Kerberos|88|AD01 e AD02,|  
|_ldap|389|AD01 e AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>Porte interne  
Le seguenti porte usate da PDW per la comunicazione interna, ma non vengono aperte per le connessioni provenienti all'esterno dell'appliance PDW.  
  
|Scopo|N. porta|Nodi|  
|-----------|-----------|---------|  
|Traffico del canale di controllo DMS|16450|ELENCO DI SCOPI CONSENTITI, CMP|  
|Traffico del canale dati DMS|16550|ELENCO DI SCOPI CONSENTITI, CMP|  
|Diagnostica interna|16650|ELENCO DI SCOPI CONSENTITI, CMP|  
|Stato di failover (DMS)|15000|ELENCO DI SCOPI CONSENTITI, CMP|  
|Stato di failover (motore)|15001|CMP|  
|Intervallo di porte dinamiche (temporaneo)|20000-65535|ELENCO DI SCOPI CONSENTITI, CMP|  
|Intervalli di porte di SQL Server (TDS)|1433, 1500-1508|ELENCO DI SCOPI CONSENTITI, CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> Creazione di tabelle esterne o origini dati esterne Usa la porta TCP 8020 per impostazione predefinita. Queste istruzioni possono essere configurate per utilizzare invece le altre porte. La porta predefinita Hortonworks JOB_TRACKER_LOCATION è 50300. L'integrazione con altri sistemi e gli strumenti possono essere richieste porte aggiuntive.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
