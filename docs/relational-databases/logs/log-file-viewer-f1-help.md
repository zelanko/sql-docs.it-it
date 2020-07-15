---
title: Guida sensibile al contesto del Visualizzatore file di log | Microsoft Docs
description: Consultare le indicazioni dalla Guida sensibile al contesto per le colonne visualizzate di frequente, le autorizzazioni e altre opzioni per il Visualizzatore file di log in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
f1_keywords:
- sql13.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: caa7cb4a5a6f5e5f2d3b951f56c3fde0b30978c2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784040"
---
# <a name="log-file-viewer-f1-help"></a>Guida sensibile al contesto del Visualizzatore file di log
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Nel Visualizzatore file di log sono visualizzate informazioni sui log relativi a molti componenti diversi. Quando il Visualizzatore file di log è aperto, selezionare i log che si desidera visualizzare nel riquadro **Seleziona log** . In ogni log vengono visualizzate le colonne appropriate per il tipo di log specifico.  
  
 I log disponibili dipendono dalla modalità di apertura del Visualizzatore file di log. Per altre informazioni, vedere [Aprire il visualizzatore file di log](../../relational-databases/logs/open-log-file-viewer.md).  
  
 Il numero di righe visualizzate per i log di controllo può essere configurato nella pagina **Esplora oggetti di SQL Server/Comandi** della finestra di dialogo **Strumenti/Opzioni** . Per le descrizioni delle colonne visualizzate per i log di controllo, vedere [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md).  
  
## <a name="options"></a>Opzioni  
 **Carica log**  
 Consente di aprire una finestra di dialogo in cui è possibile specificare un file di log da caricare.  
  
 **Export**  
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
 Consente di visualizzare un riepilogo dei filtri del file di log. Se non è stato applicato alcun filtro al file, verrà visualizzato il testo **Nessun filtro applicato**. Se è stato applicato un filtro al log, verrà visualizzato il testo **Filtra voci del log in cui:** \<filter criteria>.  
  
 **Dettagli riga selezionata**  
 Consente di selezionare una riga di evento nella parte inferiore della pagina per visualizzare dettagli aggiuntivi sulla riga. È possibile riordinare le colonne trascinandole su nuove posizioni all'interno della griglia. Le colonne possono inoltre essere ridimensionate trascinando verso destra o verso sinistra le corrispondenti barre di separazione nell'intestazione della griglia. Per adattare automaticamente le dimensioni della colonna al contenuto, fare doppio clic sulle barre di separazione nell'intestazione della griglia.  
  
 **Istanza**  
 Nome dell'istanza in cui si è verificato l'evento. Viene visualizzato come *nome computer*\\*nome istanza*.  
  
## <a name="frequently-displayed-columns"></a>Colonne generalmente visualizzate  
 **Data**  
 Visualizza la data dell'evento.  
  
 **Origine**  
 Consente di visualizzare la funzionalità di origine da cui è stato creato l'evento, ad esempio il nome del servizio, come MSSQLSERVER. Questa opzione non viene visualizzata per tutti i tipi di log.  
  
 **Messaggio**  
 Consente di visualizzare i messaggi associati all'evento.  
  
 **Tipo log**  
 Consente di visualizzare il tipo di log cui appartiene l'evento. Tutti i log selezionati vengono visualizzati nella finestra di riepilogo dei log.  
  
 **Origine log**  
 Visualizza una descrizione del log di origine in cui viene acquisito l'evento.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per accedere ai file di log per le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] online, è necessaria l'appartenenza al ruolo predefinito del server securityadmin.  
  
 Per accedere a file di log per istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline, è necessario avere accesso in lettura sia allo spazio dei nomi WMI **Root\Microsoft\SqlServer\ComputerManagement10** sia alla cartella in cui sono archiviati i file di log. Per altre informazioni, vedere la sezione Autorizzazioni dell'argomento [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzatore file di log](../../relational-databases/logs/log-file-viewer.md)   
 [Aprire il visualizzatore file di log](../../relational-databases/logs/open-log-file-viewer.md)   
 [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
