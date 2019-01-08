---
title: Connettersi all'appliance nodi - sistema di piattaforma Analitica | Microsoft Docs
description: Questo articolo illustra vari modi per connettersi a ogni nodo nell'appliance del sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f57719bae769a75d704454af03af82689715644d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506304"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Connettersi ai nodi di appliance nel sistema di piattaforma Analitica
Questo articolo illustra vari modi per connettersi a ogni nodo nell'appliance del sistema di piattaforma Analitica.  
  
## <a name="connecting-with-hadoop"></a>La connessione con Hadoop  
Prima di usare Hadoop con SQL Server PDW, chiedere all'amministratore di appliance per installare l'ambiente di Runtime Java su SQL Server PDW. Per istruzioni, vedere [configurare la connettività di PolyBase ai dati esterni &#40;sistema di piattaforma Analitica&#41; ](configure-polybase-connectivity-to-external-data.md) nella Guida operativa di Appliance.  
  
## <a name="ConnectingToIndividualNodes"></a>La connessione ai nodi delle Appliance  
Ciascuno dei nodi di appliance è possibile accedere direttamente solo in scenari di utilizzo specifico e dai tipi di utente specifico. La tabella seguente elenca ogni nodo di appliance e gli scenari in cui gli utenti si connetteranno direttamente a tale nodo.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Node**|**Scenari di accesso**|  
|Nodo di controllo|Usare un web browser per accedere alla Console di amministrazione, che viene eseguito nel nodo di controllo. Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Tutti gli strumenti e applicazioni client di connettersi al nodo di controllo, indipendentemente dal fatto che la connessione Usa Ethernet o InfiniBand.<br /><br />Per configurare una connessione Ethernet per il nodo di controllo, usare l'indirizzo IP del Cluster del nodo di controllo e la porta **17001**. Ad esempio, "192.168.0.1,17001".<br /><br />Per configurare una connessione InfiniBand al nodo di controllo, usare ***appliance_domain *-SQLCTL01** e la porta **17001**. Con ***appliance_domain *-SQLCTL01**, il server DNS appliance si connetterà il server alla rete InfiniBand attiva. Per configurare il server non appliance per utilizzare questa opzione, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).<br /><br />L'amministratore del dispositivo si connette al nodo di controllo per eseguire operazioni di gestione. Ad esempio, l'amministratore del dispositivo esegue le operazioni seguenti dal nodo di controllo:<br /><br />Configurare il sistema di piattaforma Analitica con il **dwconfig.exe** dello strumento di configurazione.|  
|Nodo di calcolo|Calcolare le connessioni di nodo vengono indirizzate dal nodo di controllo. Gli indirizzi IP dei nodi di calcolo non sono mai inseriti i comandi dell'applicazione come parametri.<br /><br />Per il caricamento, backup, copia di tabelle Remote e Hadoop, SQL Server PDW inviano o ricevono i dati direttamente in parallelo tra i nodi di calcolo e i nodi non di appliance o server. Queste applicazioni connettono con SQL Server PDW effettuando la connessione al nodo di controllo e quindi il nodo di controllo indica a SQL Server PDW per stabilire la comunicazione tra i nodi di calcolo e il server non appliance.<br /><br />Ad esempio, queste operazioni di trasferimento dei dati avvengano in parallelo con le connessioni dirette ai nodi di calcolo:<br /><br />Il caricamento dal server durante il caricamento in SQL Server PDW.<br /><br />Backup di database da SQL Server PDW al server di backup.<br /><br />Ripristino di un database dal server di backup in SQL Server PDW.<br /><br />Eseguire query sui dati Hadoop da SQL Server PDW.<br /><br />Esportazione dei dati da SQL Server PDW in una tabella esterna Hadoop.<br /><br />Copia di una tabella di SQL Server PDW a un database di SQL Server SMP remoto.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>La connessione per le reti Ethernet e InfiniBand  
I server remoti possono connettersi tramite la rete InfiniBand appliance o attraverso la rete Ethernet. Per motivi di prestazioni, il caricamento di server, server di backup e i server che riceve dati mediante **CREATE REMOTE TABLE AS SELECT** (istruzioni), in genere il trasferimento dei dati attraverso la rete InfiniBand di appliance.  
  
È possibile configurare i server non appliance per appartengono a un dominio o il proprio gruppo di lavoro dei clienti e quindi usare la propria rete cliente per connettersi a tali server e il trasferimento dei dati a essi. Inoltre, non appliance server connessi all'appliance InfiniBand hanno la possibilità di trasferire dati tra loro attraverso la rete InfiniBand di appliance; Prestare attenzione con questa perché può rallentare le prestazioni di SQL Server PDW.  
  
Ad esempio, questa istruzione aggiunge le credenziali di rete per eseguire i backup tramite InfiniBand a un server di backup che abbia un indirizzo IP InfiniBand 192.168.0.1. È il dominio di appliance *mypdw*, e l'istruzione viene eseguita dal server di backup. Prima di eseguire questa istruzione, è necessario inserire i propri parametri.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Ad esempio, un comando di caricamento verrà avviata con gli elementi seguenti:  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
