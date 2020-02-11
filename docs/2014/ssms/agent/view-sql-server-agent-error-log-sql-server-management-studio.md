---
title: Visualizzare il log degli errori di SQL Server Agent (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3835f83efff9e720f7f8631d527b9547e3b4239a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245604"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
  In questo argomento viene descritto come visualizzare il log degli errori di  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Nel Visualizzatore file di log sono visualizzate informazioni sui log relativi a molti componenti diversi. Quando il Visualizzatore file di log è aperto, selezionare i log che si desidera visualizzare nel riquadro **Seleziona log** . In ogni log vengono visualizzate le colonne appropriate per il tipo di log specifico. I log disponibili dipendono dalla modalità di apertura del Visualizzatore file di log.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per visualizzare il log degli errori di SQL Server Agent, utilizzando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
 Per ulteriori informazioni sulle autorizzazioni di Windows necessarie per l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio Agent, vedere [selezionare un account per il servizio SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-view-the-includessnoversionincludesssnoversion-mdmd-agent-error-log"></a>Per visualizzare il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server che contiene il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent da visualizzare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Log degli errori** .  
  
4.  Fare clic con il pulsante destro del mouse sul log degli errori da visualizzare e selezionare **Visualizza log agente**.  
  
     Nella finestra di dialogo **Visualizzatore file di log -**_nome_server_ sono disponibili le opzioni seguenti:  
  
     **Carica log**  
     Consente di aprire una finestra di dialogo in cui è possibile specificare un file di log da caricare.  
  
     **Esportazione**  
     Consente di aprire una finestra di dialogo in cui è possibile esportare in un file di testo le informazioni visualizzate nella griglia **Riepilogo file di log** .  
  
     **Aggiorna**  
     Consente di aggiornare la visualizzazione dei log selezionati. Il pulsante **Aggiorna** consente di leggere nuovamente i log selezionati dal server di destinazione applicando qualsiasi impostazione di filtro.  
  
     **Filter**  
     Consente di aprire una finestra di dialogo in cui è possibile specificare le impostazioni usate per filtrare il file di log, ad esempio **Connessione**, **Data**o altri criteri di filtro **generali** .  
  
     **Ricerca**  
     Consente di cercare testo specifico nel file di log. La ricerca con caratteri jolly non è supportata.  
  
     **Stop**  
     Consente di arrestare il caricamento delle voci del file di log. È ad esempio possibile utilizzare questa opzione se il caricamento di un file di log remoto o offline richiede parecchio tempo e si desidera visualizzare solo le voci più recenti.  
  
     **Riepilogo file di log**  
     Consente di visualizzare un riepilogo dei filtri del file di log. Se non è stato applicato alcun filtro al file, verrà visualizzato il testo **Nessun filtro applicato**. Se è stato applicato un filtro al log, verrà visualizzato il testo **Filtra voci del log in cui:** \<criteri di filtro>.  
  
     **Dettagli riga selezionata**  
     Consente di selezionare una riga di evento nella parte inferiore della pagina per visualizzare dettagli aggiuntivi sulla riga. È possibile riordinare le colonne trascinandole su nuove posizioni all'interno della griglia. Le colonne possono inoltre essere ridimensionate trascinando verso destra o verso sinistra le corrispondenti barre di separazione nell'intestazione della griglia. Per adattare automaticamente le dimensioni della colonna al contenuto, fare doppio clic sulle barre di separazione nell'intestazione della griglia.  
  
     **Istanza**  
     Nome dell'istanza in cui si è verificato l'evento. Viene visualizzato come nome *computer*\\*nome istanza*.  
  
     **Data**  
     Visualizza la data dell'evento.  
  
     **Origine**  
     Consente di visualizzare la funzionalità di origine da cui è stato creato l'evento, ad esempio il nome del servizio, come MSSQLSERVER. Questa opzione non viene visualizzata per tutti i tipi di log.  
  
     **Messaggio**  
     Consente di visualizzare i messaggi associati all'evento.  
  
     **Tipo di log**  
     Consente di visualizzare il tipo di log cui appartiene l'evento. Tutti i log selezionati vengono visualizzati nella finestra di riepilogo dei log.  
  
     **Origine log**  
     Visualizza una descrizione del log di origine in cui viene acquisito l'evento.  
  
5.  Al termine, fare clic su **Chiudi**.  
  
  
