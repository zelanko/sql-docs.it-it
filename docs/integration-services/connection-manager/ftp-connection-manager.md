---
title: Gestione connessione FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bb0b1a81a495639aa170b2047df3dd517fac1716
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918944"
---
# <a name="ftp-connection-manager"></a>gestione connessione FTP

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Una gestione connessione FTP consente la connessione di un pacchetto a un server FTP (File Transfer Protocol). Questa gestione connessione viene usata dall'attività FTP inclusa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Quando si aggiunge una gestione connessione FTP a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione FTP, imposta le proprietà della gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **FTP**.  
  
 Per configurare la gestione connessione FTP, procedere nel modo seguente:  
  
-   Specificare il nome e la porta del server.  
  
-   Specificare l'accesso anonimo oppure un nome utente e una password per l'autenticazione di base.  
  
    > [!IMPORTANT]  
    >  La gestione connessione FTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
-   Impostare il timeout, il numero di tentativi e la quantità di dati da copiare di volta in volta.  
  
-   Indicare se la gestione connessione FTP utilizza la modalità attiva o passiva.  
  
 A seconda della configurazione del sito FTP a cui si connette, può essere necessario modificare i seguenti valori predefiniti della gestione connessione FTP:  
  
-   La porta del server è impostata su 21. È necessario specificare la porta su cui è in ascolto il sito FTP.  
  
-   Il nome utente è impostato su "anonymous". È necessario specificare le credenziali richieste dal sito FTP.  
  
## <a name="activepassive-modes"></a>Modalità attiva e passiva  
 La gestione connessione FTP può inviare e ricevere file utilizzando la modalità attiva o passiva. Nella modalità attiva la connessione dati viene aperta dal server, mentre nella modalità passiva la connessione dati viene aperta dal client.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>Configurazione della gestione connessione FTP  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="ftp-connection-manager-editor"></a>Editor gestione connessione FTP
  Usare la finestra di dialogo **Editor gestione connessione FTP** per specificare le proprietà per la connessione a un server FTP.  
  
> [!IMPORTANT]  
>  La gestione connessione FTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 Per altre informazioni sulla gestione connessione FTP, vedere [Gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome server**  
 Consente di specificare il nome del server FTP.  
  
 **Porta server**  
 Consente di specificare il numero di porta del server FTP da utilizzare per la connessione. Il valore predefinito di questa proprietà è **21**.  
  
 **Nome utente**  
 Consente di specificare un nome utente per l'accesso al server FTP. Il valore predefinito di questa proprietà è **anonymous**.  
  
 **Password**  
 Consente di specificare una password per l'accesso al server FTP.  
  
 **Timeout (in secondi)**  
 Consente di specificare il numeri di secondi di attesa prima che si verifichi il timeout dell'attività. Il valore **0** indica un periodo di tempo infinito. Il valore predefinito di questa proprietà è **60**.  
  
 **Usa modalità passiva**  
 Consente di specificare se la connessione viene iniziata dal server o dal client. Il server inizia la connessione in modalità attiva, mentre il client attiva la connessione in modalità passiva. Il valore predefinito di questa proprietà è **active mode**.  
  
 **Tentativi**  
 Consente di specificare il numeri di tentativi eseguiti dall'attività per stabilire la connessione. Il valore **0** indica un numero di tentativi illimitato.  
  
 **Dimensioni blocco (in KB)**  
 Consente di specificare le dimensioni del blocco in KB per la trasmissione dei dati.  
  
 **Test connessione**  
 Dopo aver configurato la gestione connessione FTP, fare clic su **Test connessione**per assicurarsi che la connessione sia funzionante.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività FTP](../../integration-services/control-flow/ftp-task.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
