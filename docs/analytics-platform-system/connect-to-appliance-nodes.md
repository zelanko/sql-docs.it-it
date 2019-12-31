---
title: Connetti ai nodi Appliance
description: Questo articolo illustra i diversi modi per connettersi a ogni nodo nell'appliance del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401239"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Connettersi ai nodi Appliance nel sistema della piattaforma Analytics
Questo articolo illustra i diversi modi per connettersi a ogni nodo nell'appliance del sistema della piattaforma di analisi.  
  
## <a name="connecting-with-hadoop"></a>Connessione con Hadoop  
Prima di usare Hadoop con SQL Server PDW, richiedere all'amministratore del dispositivo di installare il Java Runtime Environment nel SQL Server PDW. Per istruzioni, vedere [configurare la connettività di base per i dati esterni &#40;sistema della piattaforma di analisi&#41;](configure-polybase-connectivity-to-external-data.md) nella Guida operativa dell'appliance.  
  
## <a name="ConnectingToIndividualNodes"></a>Connessione ai nodi Appliance  
Ogni nodo del dispositivo è accessibile direttamente solo in scenari di utilizzo specifici e in base ai tipi di utente specifici. La tabella seguente elenca ogni nodo del dispositivo e gli scenari in cui gli utenti si connetteranno direttamente al nodo.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> La modifica delle impostazioni del database o della tabella nei nodi di controllo o di calcolo senza consenso esplicito del team del prodotto o del team di supporto clienti di APS può rendere il dispositivo APS non supportato.
  
|||  
|-|-|  
|**Nodo**|**Scenari di accesso**|  
|Nodo di controllo|Usare un Web browser per accedere alla console di amministrazione, che viene eseguita nel nodo di controllo. Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Tutti gli strumenti e le applicazioni client si connettono al nodo di controllo, indipendentemente dal fatto che la connessione utilizzi Ethernet o InfiniBand.<br /><br />Per configurare una connessione Ethernet al nodo di controllo, usare l'indirizzo IP del cluster del nodo di controllo e la porta **17001**. Ad esempio, "192.168.0.1, 17001".<br /><br />Per configurare una connessione InfiniBand al nodo di controllo, usare <strong> *appliance_domain*-SQLCTL01</strong> e la porta **17001**. Con <strong> *appliance_domain*-SQLCTL01</strong>, il server DNS del dispositivo connetterà il server alla rete InfiniBand attiva. Per configurare il server non Appliance per l'uso, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).<br /><br />L'amministratore del dispositivo si connette al nodo di controllo per eseguire operazioni di gestione. Ad esempio, l'amministratore dell'Appliance esegue le operazioni seguenti dal nodo di controllo:<br /><br />Configurare il sistema di piattaforma di analisi con lo strumento di configurazione **dwconfig. exe** .|  
|Nodo di calcolo|Le connessioni del nodo di calcolo vengono indirizzate dal nodo di controllo. Gli indirizzi IP dei nodi di calcolo non vengono mai immessi nei comandi dell'applicazione come parametri.<br /><br />Per il caricamento, il backup, la copia della tabella remota e Hadoop, SQL Server PDW invia o riceve dati direttamente in parallelo tra i nodi di calcolo e i nodi o i server non Appliance. Queste applicazioni si connettono con SQL Server PDW connettendosi al nodo di controllo, quindi il nodo di controllo indirizza SQL Server PDW per stabilire la comunicazione tra i nodi di calcolo e il server non Appliance.<br /><br />Queste operazioni di trasferimento dei dati, ad esempio, si verificano in parallelo con le connessioni dirette ai nodi di calcolo:<br /><br />Caricamento dal server di caricamento a SQL Server PDW.<br /><br />Esecuzione del backup di un database da SQL Server PDW al server di backup.<br /><br />Ripristino di un database dal server di backup per SQL Server PDW.<br /><br />Esecuzione di query sui dati di Hadoop da SQL Server PDW.<br /><br />Esportazione di dati da SQL Server PDW a una tabella Hadoop esterna.<br /><br />Copia di una tabella SQL Server PDW in un database SMP SQL Server remoto.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Connessione alle reti Ethernet e InfiniBand  
I server remoti possono connettersi tramite la rete InfiniBand dell'appliance o tramite la rete Ethernet. Per motivi di prestazioni, il caricamento di server, server di backup e server che ricevono dati tramite la **creazione di tabelle remote come istruzioni SELECT** , in genere trasferiscono i dati attraverso la rete InfiniBand dell'appliance.  
  
È possibile configurare i server non Appliance in modo che appartengano al proprio gruppo di lavoro o dominio del cliente, quindi usare la propria rete clienti per connettersi a tali server e trasferire loro i dati. Inoltre, i server non Appliance connessi al dispositivo InfiniBand hanno la possibilità di trasferire i dati tra loro tramite la rete InfiniBand dell'appliance; prestare attenzione perché può rallentare le prestazioni di SQL Server PDW.  
  
Questa istruzione, ad esempio, aggiunge le credenziali di rete per l'esecuzione di backup tramite InfiniBand a un server di backup con un indirizzo IP InfiniBand 192.168.0.1. Il dominio dell'appliance è *mypdw*e l'istruzione viene eseguita dal server di backup. Prima di eseguire questa istruzione, è necessario inserire i propri parametri.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Ad esempio, un comando di caricamento inizierà con quanto segue:  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
