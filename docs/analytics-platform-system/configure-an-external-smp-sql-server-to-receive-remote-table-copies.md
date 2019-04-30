---
title: Configurare SQL Server per ricevere copie di una tabella remota - Parallel Data Warehouse | Microsoft Docs
description: Viene descritto come configurare un'istanza di Server SQL SMP esterna per ricevere copie di una tabella remota da Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ae6799d468d57dec04046b443c613823c0a8cb8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224690"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>Configurare un Server SQL SMP esterno per ricevere copie di una tabella remota - Parallel Data Warehouse
Viene descritto come configurare un'istanza esterna di SQL Server per ricevere copie di una tabella remota da Parallel Data Warehouse.  

In questo argomento descrive uno dei passaggi di configurazione per la configurazione di copia della tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere [copia di tabelle Remote](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Prima di poter configurare l'esterno di SQL Server, è necessario:  
  
-   Dispone di un sistema di Windows con SQL Server 2008 Enterprise Edition o versione successiva pronta per essere installata o già installato. Il sistema di Windows deve essere già configurato seguendo le istruzioni in [configurare un esterno Windows System per ricevere remoto tabella copie usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Un account di amministratore di Windows con la possibilità di configurare l'istanza di SQL Server e il sistema di Windows.  
  
-   Un account accesso SQL Server (se è già installato SQL Server) con la possibilità di creare gli account di accesso e concedere le autorizzazioni per i database di destinazione.  
  
## <a name="HowToSQLServer"></a>Configurare un Server SQL SMP esterno per ricevere copie di una tabella remota  
La funzionalità di copia della tabella remota copia tabelle dall'appliance SQL Server PDW in un database di Server SQL SMP esterno che è in esecuzione in un sistema di Windows. Dopo aver configurato il sistema Windows esterno per ricevere copie di una tabella remota, il passaggio successivo è installare e configurare SQL Server al sistema di Windows.  
  
Per configurare SQL Server, procedere come segue:  
  
1.  Installare SQL Server 2008 Enterprise Edition o versione successiva del sistema di Windows. Ciò è detto Server SQL SMP.  
  
2.  Configurare SQL Server per accettare connessioni TCP/IP su una porta TCP predefinita. Questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata per consentire a SQL Server PDW per la connessione al Server SQL SMP.  
  
3.  Disabilitare il firewall di Windows oppure configurare la porta TCP di SQL Server SMP, in modo che possa essere utilizzata con firewall di Windows abilitata.  
  
4.  Configurare SQL Server per consentire la modalità di autenticazione di SQL Server. Esportazione di dati paralleli sempre Usa gli account di SQL Server per l'autenticazione.  
  
5.  Determinare un account di SQL Server nel Server SQL SMP che verrà usato per l'autenticazione. Concedere il privilegio per creare, eliminare e inserire dati in tabelle nel database di destinazione per l'operazione di esportazione parallela dei dati di tale account.  
  
## <a name="BPSQLConfig"></a>Le procedure consigliate per la configurazione del Server SQL SMP per la copia della tabella remota  
Quando si configura il Server SQL SMP per ricevere copie di una tabella remota, usare le seguenti procedure consigliate per migliorare le prestazioni.  
  
1.  Seguire le procedure consigliate, come documentato nella documentazione del prodotto SQL Server. Ad esempio, abilitare la crittografia dei dati. Per altre informazioni sulla sicurezza di SQL Server, vedere [sicurezza di SQL Server](../relational-databases/security/securing-sql-server.md) su MSDN.  
  
2.  Usare il modello di recupero con registrazione minima delle operazioni bulk o semplice.  
  
    Durante il dati parallelo di operazioni di esportazione, i dati vengono inserito nella tabella di destinazione appena creato in blocco. Per ottenere prestazioni ottimali durante l'inserimento bulk, impostare il database di destinazione da usare la registrazione minima delle operazioni bulk o il modello di recupero con registrazione minima.  
  
3.  Usare l'opzione batch_size per recuperare lo spazio di log.  
  
    Anche se il recupero con registrazione minima delle operazioni bulk o semplice modelli di uso minimo la registrazione per i dati in blocco inserito, si verificano comunque alcune registrazioni. Per impedire che i file di log raggiunga dimensioni eccessivamente elevate, usare l'opzione batch_size di SQL Server per recuperare periodicamente lo spazio di log.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
