---
title: Configurare SQL Server per la ricezione di copie della tabella remota
description: Viene descritto come configurare un'istanza di SQL Server SMP esterna per ricevere copie di tabelle remote da data warehouse parallele.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401320"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>Configurare un SQL Server SMP esterno per ricevere copie della tabella remota-Parallel data warehouse
Viene descritto come configurare un'istanza di SQL Server esterna per ricevere copie di tabelle remote da data warehouse parallele.  

Questo argomento descrive uno dei passaggi di configurazione per la configurazione della copia di una tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere la pagina relativa alla [copia remota della tabella](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Prima di poter configurare il SQL Server esterno, è necessario:  
  
-   Disporre di un sistema Windows con SQL Server 2008 Enterprise Edition o una versione successiva pronta per l'installazione o l'installazione. Il sistema Windows deve essere già stato configurato in base alle istruzioni riportate in [configurare un sistema Windows esterno per la ricezione di copie della tabella remota mediante InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Un account amministratore di Windows con la possibilità di configurare l'istanza di SQL Server e il sistema Windows.  
  
-   Un account di accesso SQL Server (se SQL Server è già installato) con la possibilità di creare account di accesso e concedere autorizzazioni per i database di destinazione.  
  
## <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a><a name="HowToSQLServer"></a>Configurare un SQL Server SMP esterno per ricevere copie di tabella remota  
La funzionalità di copia della tabella remota copia le tabelle dal dispositivo SQL Server PDW a un database SMP SQL Server esterno in esecuzione su un sistema Windows. Dopo aver configurato il sistema Windows esterno per la ricezione delle copie della tabella remota, il passaggio successivo consiste nell'installare e configurare SQL Server nel sistema Windows.  
  
Per configurare SQL Server, attenersi alla procedura seguente:  
  
1.  Installare SQL Server 2008 Enterprise Edition o versione successiva nel sistema Windows. Questa operazione viene definita SQL Server SMP.  
  
2.  Configurare SQL Server per accettare le connessioni TCP/IP su una porta TCP fissa. Questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata per consentire SQL Server PDW di connettersi al SQL Server SMP.  
  
3.  Disabilitare Windows Firewall o configurare SMP SQL Server porta TCP in modo che funzioni con Windows Firewall abilitato.  
  
4.  Configurare SQL Server per consentire la modalità di autenticazione SQL Server. L'esportazione parallela dei dati usa sempre gli account SQL Server per l'autenticazione.  
  
5.  Determinare un account SQL Server nel SQL Server SMP che verrà usato per l'autenticazione. Concedere a tale account il privilegio per creare, eliminare e inserire i dati nelle tabelle del database di destinazione per l'operazione di esportazione dei dati paralleli.  
  
## <a name="best-practices-for-smp-sql-server-configuration-for-remote-table-copy"></a><a name="BPSQLConfig"></a>Procedure consigliate per la configurazione di SQL Server SMP per la copia della tabella remota  
Quando si configura il SQL Server SMP per la ricezione di copie della tabella remota, utilizzare le seguenti procedure consigliate per migliorare le prestazioni.  
  
1.  Seguire le procedure consigliate descritte in SQL Server documentazione del prodotto. Ad esempio, abilitare la crittografia dei dati. Per ulteriori informazioni sulla protezione di SQL Server, vedere la pagina relativa alla [protezione di SQL Server](../relational-databases/security/securing-sql-server.md) su MSDN.  
  
2.  Utilizzare il modello di recupero con registrazione minima delle operazioni bulk o con registrazione minima.  
  
    Durante le operazioni di esportazione dei dati paralleli, i dati vengono inseriti in blocco nella tabella di destinazione appena creata. Per ottenere prestazioni ottimali durante l'inserimento bulk, impostare il database di destinazione per l'utilizzo del modello di recupero con registrazione minima delle operazioni bulk o con registrazione minima.  
  
3.  Usare l'opzione batch_size per recuperare lo spazio del log.  
  
    Sebbene i modelli di recupero con registrazione minima delle operazioni bulk usino la registrazione minima per i dati inseriti in blocco, si verificheranno comunque alcune registrazioni. Per evitare che i file di log crescano troppo grandi, usare l'opzione SQL Server batch_size per recuperare periodicamente lo spazio del log.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
