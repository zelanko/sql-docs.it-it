---
title: Configurazione dei protocolli di rete predefiniti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 218389eaf76336e33d866f16c6b79ef54661be0b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011955"
---
# <a name="default-sql-server-network-protocol-configuration"></a>Configurazione dei protocolli di rete predefiniti di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Per una maggiore sicurezza, per alcune nuove installazioni [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] disabilita la connettività di rete. La connettività di rete che utilizza TCP/IP non viene disabilitata se si utilizza l'edizione Enterprise, Standard, Evaluation o Workgroup oppure se è presente un'installazione precedente di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] . Per tutte le installazioni è attivato il protocollo Shared Memory, che consente le connessioni locali al server. È possibile che il servizio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser venga arrestato, in base alle condizioni e alle opzioni di installazione.

Usare il nodo Configurazione di rete [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] di Gestione configurazione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] per configurare i protocolli di rete dopo l'installazione. Usare il nodo Servizi di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] di Gestione configurazione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] per configurare l'avvio automatico del servizio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser. Per altre informazioni, vedere [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


## <a name="default-configuration"></a>Configurazione di base

Nella tabella seguente viene descritta la configurazione dopo l'installazione.

|Edizione | Presenza di nuova installazione o installazione precedente | Shared Memory | TCP/IP | Named Pipes|
| -------- | -- | -- | -- | --  |  
|Enterprise | Nuova installazione | Attivato | Attivato | Disabilitate per le connessioni di rete.|
|Standard | Nuova installazione | Attivato | Attivato | Disabilitate per le connessioni di rete.|
|Web | Nuova installazione | Attivato | Attivato | Disabilitate per le connessioni di rete.|
|Developer | Nuova installazione | Attivato | Disabled | Disabilitate per le connessioni di rete.|
|Versione di valutazione | Nuova installazione | Attivato | Attivato | Disabilitate per le connessioni di rete.|
|SQL Server Express | Nuova installazione | Attivato | Disabled | Disabilitate per le connessioni di rete.|
|Tutte le edizioni | L'installazione precedente è presente, ma non viene aggiornata. | Come in una nuova installazione | Come in una nuova installazione | Come in una nuova installazione|
|Tutte le edizioni | Aggiornamento | Attivato | Impostazioni mantenute dall'installazione precedente. | Impostazioni mantenute dall'installazione precedente.|


>[!NOTE]
> Se è in esecuzione in un cluster di failover di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , l'istanza resta in attesa sulle porte specificate per ogni indirizzo IP selezionato per [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durante l'installazione di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
>[!NOTE]
> Quando si installa [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] con argomenti del prompt dei comandi, è possibile specificare i protocolli da abilitare utilizzando i parametri `TCPENABLED` e `NPENABLED` . Per altre informazioni, vedere [Installazione di SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="creating-a-connection-string"></a>Creazione di una stringa di connessione

Per esempi di stringhe di connessione, vedere gli argomenti seguenti:
* [Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Creazione di una stringa di connessione valida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="ssnoversion_md-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Impostazioni del servizio Browser

Il servizio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser può essere configurato per l'avvio automatico durante l'installazione. L'avvio automatico rappresenta l'impostazione predefinita nei casi seguenti:

* Durante l'aggiornamento di un'installazione.
* Durante l'installazione side-by-side con un'altra istanza di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
* Durante l'installazione in un cluster.
* Durante l'installazione di un'istanza denominata del motore di database che include tutte le istanze di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express.
* Durante l'installazione di un'istanza denominata di Analysis Services.

## <a name="see-also"></a>Vedere anche

[Requisiti hardware e software per l'installazione di SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[Configurazione superficie di attacco](../../relational-databases/security/surface-area-configuration.md)  



