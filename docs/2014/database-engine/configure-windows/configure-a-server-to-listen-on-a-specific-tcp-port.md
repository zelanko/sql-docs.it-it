---
title: Configurare un Server per l'ascolto su una porta TCP specifica (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: e85b1a85ab9415c76fdaeee5453c992994a286ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813587"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port-sql-server-configuration-manager"></a>Configurazione di un server per l'attesa su una porta TCP specifica (Gestione configurazione SQL Server)
  In questo argomento viene descritto come configurare un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] per essere in ascolto su una porta fissa specifica tramite Gestione configurazione SQL Server. Se abilitata, l'istanza predefinita del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rimane in attesa sulla porta TCP 1433. Le istanze denominate del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e di [!INCLUDE[ssEW](../../includes/ssew-md.md)] sono configurate per porte dinamiche. Questo significa che selezionano una porta disponibile quando viene avviato il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando ci si connette a un'istanza denominata tramite un firewall, configurare [!INCLUDE[ssDE](../../includes/ssde-md.md)] per l'ascolto su una porta specifica, in modo da consentire l'apertura della porta appropriata nel firewall.  
  
 Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!TIP]  
>  Quando si seleziona un numero di porta, vedere la pagina [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) per un elenco di numeri di porta assegnati ad applicazioni specifiche. Selezionare un numero di porta non assegnato. Per altre informazioni, vedere la pagina relativa all' [intervallo di porte dinamiche predefinite per TCP/IP modificato in Windows Vista e in Windows Server 2008](https://support.microsoft.com/kb/929851).  
  
> [!WARNING]  
>  L'ascolto viene iniziato dal motore di database su una nuova porta al momento del riavvio. Tuttavia, tramite il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser viene monitorato il Registro di sistema e viene segnalato il nuovo numero di porta appena la configurazione viene modificata, anche se non in uso da parte del motore di database. Riavviare il motore di database per garantire coerenza ed evitare errori di connessione.  
  
 **Contenuto dell'argomento**  
  
-   **Per configurare un server per l'attesa su una porta TCP specifica utilizzando:**  
  
     [Gestione configurazione SQL Server](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>Per assegnare un numero di porta TCP/IP al motore di database di SQL Server  
  
1.  Nel riquadro della console di Gestione configurazione SQL Server espandere **Configurazione di rete SQL Server** , quindi **Protocolli per \<instance name>** e infine fare doppio clic su **TCP/IP**.  
  
2.  Nella scheda **Indirizzi TCP/IP** della finestra di dialogo **Proprietà TCP/IP** vengono visualizzati vari indirizzi IP nel formato **IP1**, **IP2**e **IPAll**. Uno di tali indirizzi corrisponde all'indirizzo IP della scheda loopback, ovvero 127.0.0.1. Ulteriori indirizzi IP vengono visualizzati per ogni indirizzo IP nel computer. Fare clic con il pulsante destro del mouse su ogni indirizzo e quindi scegliere **Proprietà** per identificare l'indirizzo IP da configurare.  
  
3.  Se nella finestra di dialogo **Porte dinamiche TCP** è incluso il valore **0**, che indica che [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in attesa su porte dinamiche, eliminare tale valore.  
  
4.  Nella casella dell'area **Proprietà** **IP**_n_ immettere nella casella **Porta TCP** il numero di porta da assegnare per l'attesa a questo indirizzo IP e quindi fare clic su **OK**.  
  
5.  Nel riquadro della console fare clic su **Servizi di SQL Server**.  
  
6.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (**\<<nome istanza>**)** e scegliere **Riavvia**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà arrestato e riavviato.  
  
 Dopo la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'ascolto su una porta specifica sono disponibili tre soluzioni per connettersi a una porta specifica con un'applicazione client:  
  
-   Eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sul server per connettersi all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] specificandone il nome.  
  
-   Creare un alias sul client, specificando il numero di porta.  
  
-   Programmare il client affinché si connetta utilizzando una stringa di connessione personalizzata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare o eliminare un alias server per l'uso da parte di un client &#40;Gestione configurazione SQL Server Manager&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
  
