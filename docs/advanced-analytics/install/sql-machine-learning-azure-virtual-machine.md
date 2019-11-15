---
title: Eseguire l'installazione in una macchina virtuale di Azure
description: Eseguire soluzioni di data science e Machine Learning R e Python in una macchina virtuale SQL Server nel cloud di Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aeec25b561822e8083b89e03f0f7e74f40660f7b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727620"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Installare Machine Learning Services per SQL Server con R e Python in una macchina virtuale di Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile installare l'integrazione di R e Python con Machine Learning Services in una macchina virtuale SQL Server in Azure, eliminando le attività di installazione e configurazione. Dopo la distribuzione della macchina virtuale, le funzionalità sono pronte per l'uso.
 
Per istruzioni dettagliate, vedere [Come effettuare il provisioning di una macchina virtuale SQL Server Windows nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

Nel passaggio [Configurare le impostazioni di SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) si aggiunge la funzionalità Machine Learning all'istanza.

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