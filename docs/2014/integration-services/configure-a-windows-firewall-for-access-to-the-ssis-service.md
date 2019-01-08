---
title: Configurare un Firewall di Windows per l'accesso al servizio SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7160e4622cea397f7b300a1221797349107d38d5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369993"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>Configurare un Windows Firewall per l'accesso al servizio SSIS
    
> [!IMPORTANT]  
>  In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servizio Windows per la gestione dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] supporta il servizio per la compatibilità con le versioni precedenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile gestire oggetti come i pacchetti del server Integration Services.  
  
 Tramite il sistema windowsfirewall viene impedito a utenti non autorizzati di accedere alle risorse del computer tramite una connessione di rete. Per accedere a un'istanza di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tramite questo firewall, è necessario configurarlo in modo da consentire l'accesso.  
  
> [!IMPORTANT]  
>  Per gestire i pacchetti archiviati in un server remoto, non è necessario connettersi all'istanza del servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul server remoto in questione. Modificare, invece, il file di configurazione per il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in modo che in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] vengano visualizzati i pacchetti archiviati nel server remoto. Per altre informazioni, vedere [Configuring the Integration Services Service &#40;SSIS Service&#41;](configuring-the-integration-services-service-ssis-service.md).  
  
 Il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa il protocollo DCOM. Per altre informazioni sul funzionamento del protocollo DCOM in presenza di firewall, vedere l'articolo[Using Distributed COM with Firewalls](https://go.microsoft.com/fwlink/?LinkId=12490)(Uso di COM distribuito con i firewall) in MSDN Library.  
  
 Sono disponibili numerosi sistemi firewall. Se si esegue un firewall diverso da windowsfirewall, consultare la documentazione del firewall per informazioni specifiche al sistema in uso.  
  
 Se il firewall supporta filtri a livello di applicazione, è possibile utilizzare l'interfaccia utente disponibile in Windows per specificare le eccezioni consentite, ovvero i programmi e i servizi che non verranno bloccati dal firewall. In caso contrario, sarà necessario configurare DCOM per l'utilizzo di un set limitato di porte TCP. Nel sito Web Microsoft per cui è disponibile un collegamento più indietro in questo argomento sono disponibili informazioni sulla procedura per l'impostazione delle porte TCP da utilizzare.  
  
 Il servizio Integration Services utilizza la porta 135 e tale porta non è modificabile. È necessario aprire la porta TCP 135 per l'accesso a Gestione controllo servizi. Gestione controllo servizi esegue operazioni come l'avvio e l'arresto dei servizi [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e la trasmissione di richieste di controllo al servizio in esecuzione.  
  
 Le informazioni nella sezione seguente sono specifiche per windowsfirewall. È possibile configurare il sistema windowsfirewall tramite l'esecuzione di un comando dal prompt dei comandi oppure tramite l'impostazione delle proprietà desiderate nella finestra di dialogo relativa a windowsfirewall.  
  
 Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="configuring-a-windowsfirewall"></a>Configurazione di windowsfirewall  
 È possibile utilizzare i comandi seguenti per aprire la porta TCP 135, aggiungere MsDtsSrvr.exe all'elenco delle eccezioni e specificare l'ambito di sblocco del firewall.  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>Per configurare windowsfirewall utilizzando una finestra del prompt dei comandi  
  
1.  Eseguire il comando: `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  Eseguire il comando: `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  Per aprire il firewall per tutti i computer, inclusi quelli su Internet, sostituire scope=SUBNET con scope=ALL.  
  
 Nell'argomento seguente viene descritta la procedura per aprire la porta TCP 135, aggiungere MsDtsSrvr.exe all'elenco delle eccezioni e specificare l'ambito di sblocco del firewall tramite l'interfaccia utente di Windows.  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>Per configurare il firewall utilizzando la finestra di dialogo relativa a windowsfirewall  
  
1.  Nel Pannello di controllo fare doppio clic su **Windows Firewall**.  
  
2.  Nella finestra di dialogo **Windows Firewall** fare clic sulla scheda **Eccezioni** e quindi su **Aggiungi programma**.  
  
3.  Nella finestra di dialogo **Aggiungi programma** fare clic su **Sfoglia**, passare alla cartella Programmi\Microsoft SQL Server\100\DTS\Binn, fare clic su MsDtsSrvr.exe e quindi scegliere **Apri**. Fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi programma** .  
  
4.  Nella scheda **Eccezioni** fare clic su **Aggiungi porta**.  
  
5.  Nella finestra di dialogo **Aggiungi porta** digitare **RPC(TCP/135)** o un altro nome descrittivo nella casella **Nome**, digitare **135** nella casella **Numero porta** e quindi selezionare **TCP**.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Il servizio usa sempre la porta 135. Non è possibile specificare una porta diversa.  
  
6.  Nella finestra di dialogo **Aggiungi porta** è possibile scegliere facoltativamente **Cambia ambito** per modificare l'ambito predefinito.  
  
7.  Nella finestra di dialogo **Cambia ambito** selezionare **Solo la rete (subnet) locale** oppure digitare un elenco personalizzato e quindi fare clic su **OK**.  
  
8.  Per chiudere la finestra di dialogo **Aggiungi porta** , fare clic su **OK**.  
  
9. Per chiudere la finestra di dialogo **Windows Firewall** , fare clic su **OK**.  
  
    > [!NOTE]  
    >  Per configurare Windows Firewall, in questa procedura viene usato l'elemento **Windows Firewall** nel Pannello di controllo. L'elemento **Windows Firewall** configura il firewall solo per il profilo del percorso di rete corrente. È tuttavia anche possibile configurare Windows Firewall usando lo strumento da riga di comando **netsh** o lo snap-in [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC) denominato Windows Firewall con protezione avanzata. Per altre informazioni sull'esecuzione di questa operazione, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md)   
 [Servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md)  
  
  
