---
title: Configurare un server per l'attesa su una porta TCP specifica | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a990088feab172954f82b3be34a505202626c7d0
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132801"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port"></a>Configurare un server per l'attesa su una porta TCP specifica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento viene descritto come configurare un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] per essere in ascolto su una porta fissa specifica tramite Gestione configurazione SQL Server. Se abilitata, l'istanza predefinita del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rimane in attesa sulla porta TCP 1433. Le istanze denominate del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e di [!INCLUDE[ssEW](../../includes/ssew-md.md)] sono configurate per le [porte dinamiche](../../tools/configuration-manager/tcp-ip-properties-ip-addresses-tab.md). Questo significa che selezionano una porta disponibile quando viene avviato il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando ci si connette a un'istanza denominata tramite un firewall, configurare [!INCLUDE[ssDE](../../includes/ssde-md.md)] per l'ascolto su una porta specifica, in modo da consentire l'apertura della porta appropriata nel firewall.  

Poiché la porta 1433 è lo standard noto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], alcune organizzazioni specificano che il numero di porta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere modificato per migliorare la sicurezza. Ciò potrebbe essere utile in alcuni ambienti. Tuttavia, l'architettura TCP/IP consente a uno [scanner di porta](https://wikipedia.org/wiki/Port_scanner) di eseguire una query per le porte aperte, pertanto la modifica del numero di porta non viene considerata una misura di sicurezza affidabile.

 Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!TIP]  
>  Quando si seleziona un numero di porta, vedere la pagina [https://www.iana.org/assignments/port-numbers](https://www.iana.org/assignments/port-numbers) per un elenco di numeri di porta assegnati ad applicazioni specifiche. Selezionare un numero di porta non assegnato. Per altre informazioni, vedere la pagina relativa all' [intervallo di porte dinamiche predefinite per TCP/IP modificato in Windows Vista e in Windows Server 2008](https://support.microsoft.com/kb/929851).  
  
> [!WARNING]  
>  L'ascolto viene iniziato dal motore di database su una nuova porta al momento del riavvio. Tuttavia, tramite il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser viene monitorato il Registro di sistema e viene segnalato il nuovo numero di porta appena la configurazione viene modificata, anche se non in uso da parte del motore di database. Riavviare il motore di database per garantire coerenza ed evitare errori di connessione.  
  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>Per assegnare un numero di porta TCP/IP al motore di database di SQL Server  
  
1.  Nel riquadro della console di Gestione configurazione SQL Server espandere **Configurazione di rete SQL Server** , quindi **Protocolli per \<instance name>** e infine fare doppio clic su **TCP/IP**.  
  
    > [!NOTE]  
    >  In caso di problemi all'apertura di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).  
  
2.  Nella scheda **Indirizzi TCP/IP** della finestra di dialogo **Proprietà TCP/IP** vengono visualizzati vari indirizzi IP nel formato **IP1**, **IP2**e **IPAll**. Uno di tali indirizzi corrisponde all'indirizzo IP della scheda loopback, ovvero 127.0.0.1. Ulteriori indirizzi IP vengono visualizzati per ogni indirizzo IP nel computer. Probabilmente verranno visualizzati sia gli indirizzi IP versione 4 sia quelli IP versione 6. Fare clic con il pulsante destro del mouse su ogni indirizzo e scegliere **Proprietà** per identificare l'indirizzo IP da configurare.  
  
3.  Se nella finestra di dialogo **Porte dinamiche TCP** è incluso il valore **0**, che indica che [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in attesa su porte dinamiche, eliminare tale valore.  
  
     ![TCP_ports](../../database-engine/configure-windows/media/tcp-ports.png "TCP_ports")  
  
4.  Nella casella dell'area **Proprietà**_n_ **IP** immettere nella casella **Porta TCP** box, type the port number you want this Proprietà address to listen on, and then click **OK**. È possibile specificare più porte separandole con una virgola.

    > [!NOTE] 
    > Se l'impostazione **Attesa su tutti** nella scheda **Protocollo** è impostata su Sì, verranno usati solo i valori **Porta TCP** e **TCP Dynamic Port** (Porta dinamica TCP) nella sezione **IPAll** e le singole sezioni **IP**_n_ verranno ignorate completamente. Se l'impostazione **Attesa su tutti** è impostata su "No", le impostazioni **Porta TCP** e **TCP Dynamic Port** (Porta dinamica TCP) nella sezione **IPAll** verranno ignorate e verranno invece usate le impostazioni **Porta TCP**, **TCP Dynamic Port** (Porta dinamica TCP) e **Enabled** (Abilitata) nelle singole sezioni **IP**_n_.
    > Per ogni sezione **IP**_n_ è disponibile un'impostazione **Enabled** (Abilitata) con valore predefinito "No", a causa del quale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignora questo indirizzo IP, anche se ha una porta definita.  
  
5.  Nel riquadro della console fare clic su **Servizi di SQL Server**.  
  
6.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (**\<<nome istanza>**)** e scegliere **Riavvia**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà arrestato e riavviato.  
  
## <a name="connecting"></a>Connecting  
Dopo la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'ascolto su una porta specifica sono disponibili tre soluzioni per connettersi a una porta specifica con un'applicazione client:  
  
-   Eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sul server per connettersi all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] specificandone il nome.  
-   Creare un alias sul client, specificando il numero di porta.  
-   Programmare il client affinché si connetta utilizzando una stringa di connessione personalizzata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare o eliminare un alias server per l'uso da parte di un client &#40;Gestione configurazione SQL Server Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Servizio SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
