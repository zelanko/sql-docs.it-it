---
title: Proprietà - Protocolli per MSSQLSERVER (scheda Flag)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ff40fa868780078f2e16675b2b565a156cd41200
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087487"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>Proprietà - Protocolli per MSSQLSERVER (scheda Flag)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Quando un certificato è installato nel server, è possibile usare la scheda **Flag** della finestra di dialogo **Proprietà - Protocolli per MSSQLSERVER** per visualizzare o specificare la crittografia del protocollo e nascondere le opzioni di istanza. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere riavviato per abilitare o disabilitare l'impostazione **ForceEncryption**.  
  
 Per la crittografia delle connessioni, fornire un certificato al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Se non è installato un certificato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genererà un certificato autofirmato all'avvio dell'istanza. Questo certificato autofirmato può essere usato in sostituzione di un certificato di un'autorità di certificazione attendibile, ma non fornisce autenticazione o non ripudio.  
  
> [!CAUTION]  
>  Le connessioni Transport Layer Security (TLS), denominate in precedenza SSL (Secure Sockets Layer) crittografate tramite un certificato autofirmato non offrono sicurezza avanzata. Sono infatti suscettibili ad attacchi man-in-the-middle. Non è consigliabile affidarsi a TLS usando certificati autofirmati in un ambiente di produzione o su server connessi a Internet.  
  
 Per altre informazioni sulla crittografia, vedere "Crittografia delle connessioni a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Il processo di accesso viene sempre crittografato. Quando **ForceEncryption** è impostato su **Sì**, ogni comunicazione client/server viene crittografata e la connessione dei client a [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve essere configurata in modo da considerare attendibile l'autorità radice del certificato del server. Per altre informazioni, vedere "Procedura: Abilitazione di connessioni crittografate al [!INCLUDE[ssDE](../../includes/ssde-md.md)] (Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="cluster-servers"></a>Server di cluster  
 Se si desidera usare la crittografia in un cluster di failover, è necessario installare il certificato server contenente il nome DNS completo del server virtuale in tutti i nodi del cluster di failover. Se ad esempio si ha un cluster costituito da due nodi, denominati rispettivamente "test1. *\<società.com>* .com" e "test2. *\<società>* .com" e un server virtuale denominato "virtsql", è necessario installare un certificato per "virtsql. *\<società>* .com" in entrambi i nodi. A questo punto, è possibile selezionare la casella di controllo **ForceEncryption** in **Gestione configurazione SQL Server** per configurare il cluster di failover per la crittografia.  
  
## <a name="options"></a>Opzioni  
 **ForceEncryption**  
 Forza la crittografia del protocollo. La crittografia consente di mantenere riservati i dati convertendoli in un formato non leggibile. In tal modo, i dati risultano protetti anche nel caso in cui i pacchetti di trasmissione vengano visualizzati durante il processo di trasferimento. Per usare il binding di canale, impostare **Forza crittografia** su **Attivata** e configurare **Protezione estesa** nella scheda **Avanzate** .  
  
 **HideInstance**  
 Impedisce al servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser di esporre l'istanza corrente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ai computer client che tentano di individuarla tramite il pulsante **Sfoglia** . Nel caso di istanze denominate nel server, ai fini della connessione è necessario che le applicazioni specifichino le informazioni sull'endpoint del protocollo, ad esempio il numero di porta o il nome di named pipe, quale **tcp:server,5000**. Per altre informazioni, vedere [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md).  
  
 Per altre informazioni, vedere "Procedura: Abilitare connessioni crittografate al motore di database (Gestione configurazione SQL Server)" nella documentazione online.  
  
  
