---
title: Eseguire l'installazione in una macchina virtuale di Azure
description: Eseguire soluzioni di data science e Machine Learning di Python e R con Machine Learning Services per SQL Server in una macchina virtuale nel cloud di Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d81237f67c82fd7cc8b9259fcd7a0202ffb7fd4b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75776592"
---
# <a name="install-sql-server-machine-learning-services-with-python-and-r-on-an-azure-virtual-machine"></a>Installare Machine Learning Services per SQL Server con Python e R in una macchina virtuale di Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Informazioni su come installare Python e R con Machine Learning Services per SQL Server in una macchina virtuale in Azure. In questo modo vengono eliminate le attività di installazione e configurazione per Machine Learning Services.

A tale scopo, seguire questa procedura:

1. Provisioning della macchina virtuale di SQL Server in Azure
1. Sbloccare il firewall
1. Abilitare i callback ODBC per i client remoti
1. Aggiungere protocolli di rete

## <a name="provision-sql-server-virtual-machine-in-azure"></a>Provisioning della macchina virtuale di SQL Server in Azure

Per istruzioni dettagliate, vedere [Come effettuare il provisioning di una macchina virtuale SQL Server Windows nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision). 

Nel passaggio [Configurare le impostazioni di SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) si aggiunge la funzionalità Machine Learning Services all'istanza.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Sbloccare il firewall

Per impostazione predefinita, il firewall della macchina virtuale di Azure include una regola che blocca l'accesso alla rete per gli account utente locali.

È necessario disabilitare questa regola per consentire l'accesso all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un client di data science remoto.  In caso contrario, il codice di Machine Learning non può essere eseguito nei contesti di calcolo che usano l'area di lavoro della macchina virtuale.

Per consentire l'accesso da client di data science remoti:

1. Nella macchina virtuale aprire Windows Firewall con protezione avanzata.
2. Selezionare **Regole in uscita**
3. Disabilitare la regola seguente:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Abilitare i callback ODBC per i client remoti

Se si prevede che i client che chiamano il server debbano eseguire query ODBC nell'ambito delle soluzioni di Machine Learning, è necessario assicurarsi che Launchpad possa effettuare chiamate ODBC per conto del client remoto. 

A tale scopo, è necessario consentire agli account di lavoro SQL usati da Launchpad di accedere all'istanza. Per altre informazioni, vedere [Aggiungere SQLRUserGroup come utente del database](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Aggiungere protocolli di rete

+ Abilitare Named Pipes
  
  Attualmente, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa il protocollo Named Pipes per le connessioni tra i computer client e server e per alcune connessioni interne. Se il protocollo Named Pipes non è abilitato, è necessario installarlo e abilitarlo sia nella macchina virtuale di Azure che nei client di data science che si connettono al server.
  
+ Abilitare TCP/IP

  Il protocollo TCP/IP è necessario per le connessioni loopback. Se viene visualizzato l'errore "DBNETLIB: Server SQL inesistente o accesso negato", abilitare TCP/IP nella macchina virtuale che supporta l'istanza.