---
title: Installare il linguaggio R e le funzionalità di Python in una macchina virtuale di Azure - servizi di SQL Server Machine Learning
description: Eseguire l'analisi scientifica dei dati di R e Python e machine learning solutions in una macchina virtuale di SQL Server nel cloud di Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 01fb7962a5be08f40fe1c790b335c24d34979a2a
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141470"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Installare servizi di SQL Server Machine Learning con R e Python in una macchina virtuale di Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile installare l'integrazione di R e Python con i servizi di Machine Learning in una macchina virtuale di SQL Server in Azure, eliminando le attività di installazione e configurazione. Dopo aver distribuita la macchina virtuale, le funzionalità sono pronte per l'uso.
 
Per istruzioni dettagliate, vedere [come eseguire il provisioning di una macchina virtuale di Windows SQL Server nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

Il [impostazioni di configurazione SQL server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) passaggio è aggiungere apprendimento per l'istanza.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Sbloccare il firewall

Per impostazione predefinita, il firewall nella macchina virtuale di Azure include una regola che blocca accesso alla rete per gli account utente locali.

È necessario disabilitare questa regola per assicurarsi che sia possibile accedere la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza da un client di analisi scientifica dei dati remota.  Codice di apprendimento automatico in caso contrario, non è possibile eseguire in contesti di calcolo che usano l'area di lavoro della macchina virtuale.

Per abilitare l'accesso dai client di analisi scientifica dei dati remota:

1. Nella macchina virtuale aprire Windows Firewall con protezione avanzata.
2. Selezionare **Regole in uscita**
3. Disabilitare la regola seguente:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Abilitare i callback ODBC per i client remoti

Se si prevede che i client che chiamano il server saranno necessario eseguire query ODBC come parte del loro soluzioni di machine learning, è necessario assicurarsi che Launchpad possa effettuare chiamate ODBC per conto del client remoto. 

A tale scopo, è necessario consentire agli account di lavoro SQL usati da Launchpad di accedere all'istanza. Per altre informazioni, vedere [aggiungere SQLRUserGroup come utente del database](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Aggiungere protocolli di rete

+ Abilitare Named Pipes
  
  Attualmente, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa il protocollo Named Pipes per le connessioni tra i computer client e server e per alcune connessioni interne. Se il protocollo Named Pipes non è abilitato, è necessario installarlo e abilitarlo sia nella macchina virtuale di Azure che nei client di data science che si connettono al server.
  
+ Abilitare TCP/IP

  È necessaria per le connessioni loopback TCP/IP. Se viene visualizzato l'errore "DBNETLIB. SQL Server non esiste o accesso negato", abilitare TCP/IP sulla macchina virtuale che supporta l'istanza.