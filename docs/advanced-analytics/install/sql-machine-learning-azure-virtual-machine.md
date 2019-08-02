---
title: Installare il linguaggio R e le funzionalità Python in una macchina virtuale di Azure
description: Esegui soluzioni R e Python data science e Machine Learning in una macchina virtuale SQL Server nel cloud di Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7aa37c3ec72390d76ecf9e939916f9641187956
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715878"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Installare SQL Server Machine Learning Services con R e Python in una macchina virtuale di Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile installare l'integrazione di R e Python con Machine Learning Services in una macchina virtuale SQL Server in Azure, eliminando le attività di installazione e configurazione. Una volta distribuita la macchina virtuale, le funzionalità sono pronte per l'uso.
 
Per istruzioni dettagliate, vedere [come effettuare il provisioning di una macchina virtuale Windows SQL Server nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

Il passaggio [Configura impostazioni SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) consente di aggiungere machine learning all'istanza.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Sbloccare il firewall

Per impostazione predefinita, il firewall nella macchina virtuale di Azure include una regola che blocca l'accesso alla rete per gli account utente locali.

È necessario disabilitare questa regola per assicurarsi che sia possibile accedere all' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza da un client di Data Science remoto.  In caso contrario, il codice di apprendimento automatico non può essere eseguito nei contesti di calcolo che usano l'area di lavoro della macchina virtuale.

Per abilitare l'accesso dai client di data science remoto:

1. Nella macchina virtuale aprire Windows Firewall con protezione avanzata.
2. Selezionare **Regole in uscita**
3. Disabilitare la regola seguente:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Abilitare i callback ODBC per i client remoti

Se si prevede che i client che chiamano il server dovranno eseguire query ODBC come parte delle proprie soluzioni di apprendimento automatico, è necessario assicurarsi che la finestra di avvio possa effettuare chiamate ODBC per conto del client remoto. 

A tale scopo, è necessario consentire agli account di lavoro SQL usati da Launchpad di accedere all'istanza. Per altre informazioni, vedere [aggiungere SQLRUserGroup come utente del database](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Aggiungere protocolli di rete

+ Abilitare Named Pipes
  
  Attualmente, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa il protocollo Named Pipes per le connessioni tra i computer client e server e per alcune connessioni interne. Se il protocollo Named Pipes non è abilitato, è necessario installarlo e abilitarlo sia nella macchina virtuale di Azure che nei client di data science che si connettono al server.
  
+ Abilitare TCP/IP

  TCP/IP è necessario per le connessioni loopback. Se viene ricevuto l'errore "DBNETLIB; SQL Server non esiste o l'accesso è negato ", abilitare TCP/IP nella macchina virtuale che supporta l'istanza di.