---
title: Configurazione del firewall PDW
description: La pagina Firewall del SQL Server PDW Configuration Manager consente di abilitare o disabilitare le regole del firewall che consentono o impediscono l'accesso a porte specifiche nell'appliance del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400878"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configurazione Parallel data warehouse firewall nel sistema della piattaforma Analytics

La pagina **Firewall** del SQL Server PDW Configuration Manager consente di abilitare o disabilitare le regole del firewall che consentono o impediscono l'accesso a porte specifiche nell'appliance del sistema della piattaforma di analisi.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Per gestire le porte e le regole del firewall per i nodi Appliance  
  
1.  Avviare il Configuration Manager. Per ulteriori informazioni, vedere [la pagina relativa all'avvio del&#41;di sistema della piattaforma Configuration Manager &#40;Analytics ](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro del Configuration Manager espandere **topologia data warehouse parallela**, quindi fare clic su **Firewall**.  
  
3.  Individuare la porta o la regola del firewall da aggiornare nell'elenco configurazione, quindi selezionare o deselezionare la casella accanto a tale elemento. In questo elenco sono mostrate solo le opzioni configurabili dall'amministratore SQL Server PDW, incluse le porte di apertura e chiusura nei nodi con interfaccia esterna.  
  
4.  Fare clic su **applica** per salvare le modifiche.  
  
![Firewall PDW strumento DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Porte esterne  
Le porte seguenti vengono aperte per le connessioni client provenienti dall'esterno di PDW.  
  
|Scopo|Porta #|Nodi|  
|-----------|-----------|---------|  
|Accesso client SQL per PDW (TDS)|17001|CTL|  
|Accesso client loader (dwloader & SSIS)|8001|CTL|  
|Accesso tramite Desktop remoto|3389|CTL, CMP|  
|BinaryLoaderDataChannel SSIS|16551|CTL|  
|BinaryLoaderDataChannel dwloader|16551|CMP|  
|Connessioni crittografate SSL (per le comunicazioni interne, per accedere alla console di amministrazione)|443|Tutti i nodi|  
|Flusso di controllo del carico SQL Server PDW-credenziali di Windows|8002|CTL|  
|_Kerberos|88|AD01 e AD02,|  
|_ldap|389|AD01 e AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>Porte interne  
Le porte seguenti vengono usate da PDW per la comunicazione interna, ma non sono aperte per le connessioni provenienti dall'esterno del dispositivo PDW.  
  
|Scopo|Porta #|Nodi|  
|-----------|-----------|---------|  
|Traffico del canale di controllo DMS|16450|CTL, CMP|  
|Traffico del canale dati DMS|16550|CTL, CMP|  
|Diagnostica interna|16650|CTL, CMP|  
|Stato failover (DMS)|15000|CTL, CMP|  
|Stato failover (motore)|15001|CMP|  
|Intervallo di porte dinamico (temporaneo)|20000-65535|CTL, CMP|  
|Intervalli di porte SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> Per impostazione predefinita, la creazione di tabelle esterne o origini dati esterne usa la porta TCP 8020. Queste istruzioni possono essere configurate in modo da usare invece altre porte. La porta predefinita di Hortonworks JOB_TRACKER_LOCATION è 50300. L'integrazione con altri sistemi e strumenti potrebbe richiedere porte aggiuntive.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
