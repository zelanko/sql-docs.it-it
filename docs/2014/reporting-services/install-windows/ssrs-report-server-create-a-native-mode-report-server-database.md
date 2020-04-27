---
title: Creare un database del server di report in modalità nativa (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- databases [Reporting Services], creating
ms.assetid: 81b9f4ad-800b-4688-8b47-a5a83dc8ff10
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ae243786119823a7be4a093fcfef232f58d8492
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108680"
---
# <a name="create-a-native-mode-report-server-database--ssrs-configuration-manager"></a>Creare un database del server di report in modalità nativa (Gestione configurazione SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa viene utilizzato un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'archiviazione interna. Il database è obbligatorio e viene utilizzato per archiviare report pubblicati, modelli, origini dati condivise, dati di sessione, risorse e metadati del server.  
  
 Per creare un database del server di report o modificare le credenziali o la stringa di connessione, utilizzare le opzioni disponibili nella pagina Database di Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa|  
  
## <a name="when-to-create-or-configure-the-report-server-databases"></a>Casi in cui creare o configurare i database del server di report  
 È necessario creare e configurare il database del server di report se il server di report è stato installato in modalità "solo file".  
  
 Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato installato nella configurazione predefinita per la modalità nativa, il database del server di report è stato creato e configurato automaticamente durante l'installazione dell'istanza del server di report. È possibile utilizzare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per visualizzare o modificare le impostazioni configurate dal programma di installazione.  
  
##  <a name="before-you-start"></a><a name="rsdbrequirements"></a> Prima di iniziare  
 La creazione o la configurazione di un database del server di report è un processo che comprende diversi passaggi. Prima di creare il database del server di report, determinare il modo in cui effettuare le operazioni seguenti:  
  
 Selezionare un server di database  
 Verificare le versioni supportate della [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e le edizioni supportate nell'argomento [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md).  
  
 Abilitare le connessioni TCP/IP  
 Abilitare le connessioni TCP/IP per il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Il protocollo TCP/IP non è abilitato per impostazione predefinita in alcune edizioni del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . In questo argomento sono incluse le indicazioni necessarie per eseguire l'attivazione.  
  
 Aprire la porta per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Per un server remoto, se si utilizza un software firewall, è necessario aprire la porta su cui è in ascolto il [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Determinare le credenziali del server di report  
 Determinare la modalità utilizzata dal server di report per la connessione ai relativi database. Tra i tipi di credenziali possibili sono inclusi l'account utente di dominio, l'account utente del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'account del servizio del server di report.  
  
 Tali credenziali vengono crittografate e archiviate nel file RSReportServer.config. Il server di report utilizza le credenziali per le connessioni al database del server di report in corso. Se si desidera utilizzare un account utente di Windows o un account utente del database, verificare di specificarne uno già esistente. Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] crea un account di accesso e imposta le autorizzazioni necessarie, ma non crea un account per l'utente. Per ulteriori informazioni, vedere [configurare una connessione del database del server di Report &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 Determinare la lingua del server di report  
 Scegliere una lingua da specificare per il server di report. I nomi dei ruoli predefiniti, le descrizioni e le cartelle dei report personali non verranno visualizzati in lingue diverse quando gli utenti si connettono al server tramite versioni del browser in altre lingue.  
  
 Controllare le credenziali per creare il database ed effettuarne il provisioning  
 Verificare che le credenziali dell'account in uso dispongano dell'autorizzazione necessaria per creare database nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Tali credenziali vengono usate per una connessione occasionale per creare il database del server di report e **RSExecRole**. Se non è disponibile alcun account di accesso, verrà creato un account utente di accesso al database per l'account utilizzato dal server di report per la connessione al database. È possibile connettersi tramite l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per accedere al sistema oppure è possibile immettere un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-enable-access-to-a-remote-report-server-database"></a>Per abilitare l'accesso a un database del server di report remoto  
  
1.  Se si utilizza un'istanza remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , accedere al server di database per verificare o abilitare le connessioni TCP/IP.  
  
2.  Fare clic sul menu **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, **Strumenti di configurazione**, quindi **Gestione configurazione SQL Server**.  
  
3.  Aprire **SQL Server configurazione di rete**.  
  
4.  Selezionare l'istanza.  
  
5.  Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **abilitato**.  
  
6.  Riavviare il servizio.  
  
7.  Aprire il software firewall e la porta di attesa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per l'istanza predefinita, il numero di porta per le connessioni TCP/IP è in genere 1433. Per altre informazioni, vedere [Configurare Windows Firewall per l'accesso al motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-create-a-local-report-server-database"></a>Per creare un database del server di report locale  
  
1.  Avviare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi all'istanza del server di report per cui si desidera creare il database. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Nella pagina Database fare clic su **Cambia database**.  
  
3.  Fare clic su **Crea un nuovo database del server di report**, quindi scegliere **Avanti**.  
  
4.  Connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che verrà utilizzata per creare e ospitare il database del server di report.  
  
    1.  Immettere l'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che si desidera utilizzare. Nella procedura guidata verrà visualizzato un [!INCLUDE[ssDE](../../includes/ssde-md.md)] locale, se disponibile, eseguito come istanza predefinita. In caso contrario, è necessario immettere il server e l'istanza da utilizzare. Le istanze denominate vengono specificate nel formato \<nomeserver>\\<nomeistanza\>.  
  
    2.  Immettere le credenziali utilizzate per una connessione occasionale al [!INCLUDE[ssDE](../../includes/ssde-md.md)] allo scopo di creare i database del server di report. Per ulteriori informazioni sull'utilizzo di tali credenziali, vedere [Operazioni preliminari](#rsdbrequirements) in questo argomento.  
  
    3.  Fare clic su **Test connessione** per convalidare la connessione al server.  
  
    4.  Fare clic su **Avanti**.  
  
5.  Specificare le proprietà utilizzate per creare il database. Per ulteriori informazioni sull'utilizzo di tali proprietà, vedere [Operazioni preliminari](#rsdbrequirements) in questo argomento.  
  
    1.  Digitare il nome del database del server di report. Insieme al database primario verrà creato un database temporaneo. Utilizzare un nome descrittivo che semplifichi l'individuazione della modalità di utilizzo del database. Si noti che il nome specificato verrà utilizzato per tutta la durata del database. Una volta creato, non è possibile rinominare un database del server di report.  
  
    2.  Selezionare la lingua in cui si desidera visualizzare le definizioni dei ruoli e la cartella dei report personali.  
  
    3.  La modalità del server di report è sempre impostata su **Nativa**.  
  
    4.  Fare clic su **Avanti**.  
  
6.  Specificare le credenziali utilizzate dal server di report per la connessione al database del server di report.  
  
    1.  Specificare il tipo di autenticazione:  
  
         Selezionare **Credenziali database** per connettersi utilizzando un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] già definito. L'utilizzo di credenziali per l'accesso al database è consigliato se il server di report è installato in un computer appartenente a un dominio diverso o non trusted o è protetto da un firewall.  
  
         Selezionare **Credenziali di Windows** se si usa un account utente di dominio con privilegi minimi che ha l'autorizzazione necessaria per accedere al computer e al server di database.  
  
         Selezionare **Credenziali del servizio** se si desidera che il server di report si connetta tramite l'account del servizio. Se si seleziona questa opzione, il server si connette utilizzando la sicurezza integrata e le credenziali non verranno crittografate o archiviate.  
  
    2.  Fare clic su **Avanti**.  
  
7.  Esaminare le informazioni incluse nella pagina Riepilogo per verificare che le impostazioni siano corrette, quindi scegliere **Avanti**.  
  
8.  Verificare la connessione facendo clic su un URL nella pagina URL server di report o URL Gestione report. Perché il test abbia esito positivo, è necessario che gli URL siano stati definiti. Se la connessione al database del server di report è valida, in una finestra del browser verrà visualizzata la gerarchia di cartelle del server di report o Gestione report. Per altre informazioni, vedere [Verificare un'installazione di Reporting Services](verify-a-reporting-services-installation.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare una connessione al database del server di report &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Database &#40;modalità nativa SSRS&#41;](../../sql-server/install/database-ssrs-native-mode.md)   
 [Gestire un server di report Reporting Services in modalità nativa](../report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
