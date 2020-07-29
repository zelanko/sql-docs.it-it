---
title: Proprietà del nuovo passaggio di processo (pagina Generale)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 44b333c1865046f779581265fb49186810f8944c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731404"
---
# <a name="job-step-properties---new-job-step-general-page"></a>Proprietà passaggio processo - Nuovo passaggio di processo (pagina Generale)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le proprietà di un passaggio di processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o per definirne uno nuovo.  
  
Per passare a questa pagina, in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] espandere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, fare clic con il pulsante destro del mouse su **Processi**, scegliere **Nuovo processo**, selezionare la pagina **Passaggi** e scegliere **Nuovo**. È anche possibile passare a questa pagina facendo clic con il pulsante destro del mouse su un processo in Esplora oggetti, scegliendo **Proprietà**, selezionando la pagina **Passaggi** e scegliendo **Nuovo**, **Inserisci**o **Modifica**.  
  
## <a name="options"></a>Opzioni  
**Nome passaggio**  
Consente di impostare il nome del passaggio del processo.  
  
**Tipo**  
Consente di impostare il sottosistema utilizzato dal passaggio del processo. In base al sottosistema scelto, le opzioni visualizzate per la definizione del passaggio del processo sono diverse.  
  
**Esegui come**  
Consente di impostare l'account proxy per il passaggio del processo. I membri del ruolo predefinito del server sysadmin possono specificare anche l' **account del servizio SQL Agent**.  
  
**Database**  
Imposta il database in cui viene eseguito il passaggio di processo. Questa opzione non è disponibile per tutti i tipi di passaggio di processo.  
  
**Comando**  
Consente di impostare il comando eseguito dal passaggio del processo.  
  
## <a name="options-for-transact-sql-job-steps"></a>Opzioni per i passaggi del processo Transact-SQL  
**Apri**  
Consente di caricare il comando da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato negli Appunti.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
**Analizza**  
Consente di verificare la sintassi del comando.  
  
## <a name="options-for-activex-script-job-steps"></a>Opzioni per i passaggi del processo Script ActiveX  
  
> [!IMPORTANT]
> Il sottosistema di scripting ActiveX verrà rimosso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.  
  
**VBScript**  
Consente di specificare [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Basic Scripting Edition come linguaggio per i passaggi del processo.  
  
**JScript**  
Consente di specificare JScript come linguaggio per i passaggi del processo.  
  
**Altri**  
Consente di digitare il nome del linguaggio per i passaggi del processo scritti in un altro linguaggio di scripting.  
  
**Apri**  
Consente di caricare il comando da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Opzioni per i passaggi del processo Sistema operativo (CmdExec)  
**Elabora codice di uscita di un comando eseguito correttamente**  
Consente di digitare il codice di uscita restituito dal comando per indicare il corretto completamento.  
  
**Apri**  
Consente di caricare il comando da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-powershell-job-steps"></a>Opzioni per i passaggi di processo di PowerShell  
**Apri**  
Consente di caricare lo script da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo dello script.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-replication-distributor-job-steps"></a>Opzioni per i passaggi del processo Server di distribuzione repliche  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-replication-merge-job-steps"></a>Opzioni per i passaggi del processo Merge repliche  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Opzioni per i passaggi del processo Lettura coda repliche  
**Database**  
Database da utilizzare per il passaggio del processo.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-replication-snapshot-job-steps"></a>Opzioni per i passaggi del processo Snapshot repliche  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>Opzioni per i passaggi del processo Lettura log delle transazioni di replica  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>Opzioni per i passaggi del processo Comando di SQL Server Analysis Services  
**Server**  
Consente di selezionare il server in cui viene eseguito il passaggio del processo.  
  
**Apri**  
Consente di caricare il comando da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>Opzioni per i passaggi del processo Query di SQL Server Analysis Services  
**Server**  
Consente di selezionare il server in cui viene eseguito il passaggio del processo.  
  
**Database**  
Database da utilizzare per il passaggio del processo.  
  
**Apri**  
Consente di caricare il comando da un file.  
  
**Seleziona tutto**  
Consente di selezionare il testo del comando.  
  
**Copia**  
Consente di copiare il testo selezionato.  
  
**Incolla**  
Consente di incollare il contenuto degli Appunti.  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Opzioni per i passaggi del processo di esecuzione del pacchetto Integration Services  
  
### <a name="general-tab"></a>Scheda Generale  
Consente di specificare la posizione del pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis_md.md)]) e il metodo di autenticazione da utilizzare. In questa scheda sono disponibili le opzioni seguenti.  
  
**Origine pacchetto**  
Consente di specificare la posizione in cui è archiviato il pacchetto [!INCLUDE[ssIS](../../includes/ssis_md.md)] . Selezionare una delle opzioni seguenti:  
  
-   **SQL Server**  
  
-   **File system**  
  
-   **Archivio pacchetti SSIS**  
  
**Server**  
Consente di digitare il nome del server in cui è archiviato il pacchetto [!INCLUDE[ssIS](../../includes/ssis_md.md)] . Questa opzione è disponibile solo se è impostato **SQL Server** o **Archivio pacchetti SSIS** come **Origine pacchetto**.  
  
**Usa autenticazione di Windows**  
Consente di accedere a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows.  
  
**Usa autenticazione di SQL Server**  
Consente di accedere a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona questo metodo di autenticazione, immettere il **Nome utente** e la **Password corretti**.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] L'autenticazione è disponibile per garantire la compatibilità con le versioni precedenti. Per un livello di sicurezza migliore, utilizzare l'autenticazione di Windows, se possibile.  
  
**Pacchetto**  
Consente di digitare la posizione del pacchetto.  
  
> [!IMPORTANT]  
> Per pacchetti [!INCLUDE[ssIS](../../includes/ssis_md.md)] protetti da password, fare clic sulla scheda **Configurazioni** e immettere la password nella finestra di dialogo **Password pacchetto** . In caso contrario, il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in cui viene eseguito il pacchetto protetto da password avrà esito negativo.  
  
### <a name="configurations-tab"></a>Scheda Configurazioni  
Consente di specificare le opzioni di configurazione per il pacchetto [!INCLUDE[ssIS](../../includes/ssis_md.md)] . In questa scheda sono disponibili le opzioni seguenti.  
  
**File di configurazione**  
Consente di elencare i file di configurazione per il pacchetto.  
  
**Aggiungere**  
Consente di aggiungere un file di configurazione per il pacchetto.  
  
**Rimuovi**  
Consente di rimuovere un file di configurazione per il pacchetto.  
  
**Sposta su**  
Consente di spostare il file di configurazione selezionato verso l'alto.  
  
**Sposta giù**  
Consente di spostare il file di configurazione selezionato verso il basso.  
  
### <a name="command-files-tab"></a>Scheda File di comando  
Consente di selezionare i file di comando per il pacchetto. I file di comando vengono elaborati in base all'ordine in cui vengono visualizzati nell'elenco. In questa scheda sono disponibili le opzioni seguenti.  
  
**File di comando**  
Consente di elencare i file di comando per il pacchetto.  
  
**Aggiungere**  
Consente di aggiungere un file di comando.  
  
**Rimuovi**  
Consente di rimuovere il file di comando selezionato.  
  
**Sposta su**  
Consente di spostare il file di comando selezionato verso l'alto.  
  
**Sposta giù**  
Consente di spostare il file di comando selezionato verso il basso.  
  
### <a name="data-sources-tab"></a>Scheda Origini dati  
Consente di visualizzare le origini dei dati specificate nel pacchetto.  
  
**Gestione connessione**  
Consente di visualizzare il nome dell'origine dei dati.  
  
**Descrizione**  
Consente di visualizzare la descrizione dell'origine dei dati.  
  
**Stringa di connessione**  
Consente di visualizzare la stringa di connessione per l'origine dei dati.  
  
### <a name="execution-options-tab"></a>Scheda Opzioni di esecuzione  
Consente di visualizzare o modificare le opzioni di esecuzione per il pacchetto.  
  
**Interrompi il pacchetto in caso di avvisi di convalida**  
Selezionare questa opzione per interrompere l'esecuzione del pacchetto in caso di avvisi di convalida.  
  
**Convalida pacchetto senza esecuzione**  
Selezionare questa opzione affinché il passaggio del processo esegua la convalida, ma non l'esecuzione, del pacchetto.  
  
**Numero massimo di file eseguibili simultanei**  
Numero massimo di file eseguibili che è possibile eseguire simultaneamente.  
  
**Abilita checkpoint pacchetto**  
Selezionare questa opzione affinché il passaggio del processo utilizzi i checkpoint del pacchetto.  
  
**File del checkpoint**  
Consente di digitare il nome del file del checkpoint del pacchetto.  
  
**...**  
Scegliere Sfoglia per individuare il file del checkpoint del pacchetto.  
  
**Ignora opzioni di riavvio**  
Selezionare questa opzione per specificare opzioni di riavvio per il passaggio del processo diverse da quelle specificate nel pacchetto.  
  
**Opzione di riavvio**  
Consente di selezionare l'azione da intraprendere al riavvio del pacchetto.  
  
### <a name="logging-tab"></a>Scheda Registrazione  
Consente di visualizzare o modificare i provider di log per il pacchetto.  
  
**Provider di log**  
Consente di selezionare il ClassID per il provider di log.  
  
**Stringa di configurazione**  
Consente di digitare la stringa di configurazione per il provider di log.  
  
**Rimuovi**  
Consente di rimuovere il provider di log.  
  
### <a name="set-values-tab"></a>Scheda Imposta valori  
Consente di visualizzare o modificare i valori delle proprietà per il pacchetto.  
  
**Percorso proprietà**  
Consente di visualizzare o modificare il percorso per la proprietà.  
  
**Valore**  
Consente di visualizzare o modificare il valore della proprietà.  
  
**Rimuovi**  
Consente di rimuovere la proprietà.  
  
### <a name="verification-tab"></a>Scheda Verifica  
Consente di selezionare le opzioni di verifica per il passaggio del processo.  
  
**Esegui solo pacchetti firmati**  
Consente di eseguire solo i pacchetti firmati. Se questa opzione è selezionata, il passaggio del processo viene interrotto se il pacchetto non è firmato.  
  
**Verifica build pacchetto**  
Consente di eseguire solo i pacchetti con un numero di build specifico. Se questa opzione è selezionata, il passaggio del processo viene interrotto se il pacchetto non dispone del numero di build specifico.  
  
**Build**  
Consente di digitare il numero di build del pacchetto.  
  
**Verifica ID pacchetto**  
Consente di eseguire solo i pacchetti con un ID specifico. Se questa opzione è selezionata, il passaggio del processo viene interrotto se il pacchetto non dispone dell'ID specificato.  
  
**ID pacchetto**  
Consente di digitare l'ID del pacchetto.  
  
**Verifica ID versione**  
Consente di eseguire solo i pacchetti con un ID versione specifico. Se questa opzione è selezionata, il passaggio del processo viene interrotto se il pacchetto non dispone dell'ID versione specificato.  
  
**ID versione**  
Consente di digitare l'ID di versione.  
  
### <a name="command-line-tab"></a>Scheda Riga di comando  
Consente di specificare le opzioni della riga di comando per il pacchetto. In questa scheda sono disponibili le opzioni seguenti.  
  
**Ripristina opzioni originali**  
Consente di utilizzare le opzioni della riga di comando impostate in questa finestra di dialogo.  
  
**Modifica riga di comando manualmente**  
Consente di specificare le opzioni nella finestra della riga di comando.  
  
**Riga di comando**  
Consente di digitare le opzioni della riga di comando da utilizzare per il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
[Gestire passaggi di processo](../../ssms/agent/manage-job-steps.md)  
[Processi di SQL Server Agent per i pacchetti](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)  
[Amministrazione degli agenti di replica](../../relational-databases/replication/agents/replication-agent-administration.md)  
  
