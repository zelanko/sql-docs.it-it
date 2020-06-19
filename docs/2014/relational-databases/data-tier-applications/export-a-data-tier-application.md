---
title: Esportare un'applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.exportdac.settings.f1
- sql12.swb. exportdac.settings.f1
- sql12.swb.exportdac.welcome.f1
- sql12.swb. exportdac.summary.f1
- sql12.swb.exportdac.progress.f1
- sql12.swb.exportdac.summary.f1
- sql12.swb.exportdac.results.f1
- sql12.swb. exportdac.results.f1
helpviewer_keywords:
- How to [DAC], export
- wizard [DAC], export
- export DAC
- data-tier application [SQL Server], export
ms.assetid: 61915bc5-0f5f-45ac-8cfe-3452bc185558
author: stevestein
ms.author: sstein
ms.openlocfilehash: d73724cd1aebd1d06048f634da3a1ad32ff8e49c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970251"
---
# <a name="export-a-data-tier-application"></a>Esportazione di un'applicazione livello dati
  L'esportazione di un database o di un'applicazione livello dati distribuita crea un file di esportazione contenente sia le definizioni degli oggetti del database che tutti i dati contenuti nelle tabelle. Il file di esportazione può quindi essere importato in un'altra istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]o in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Le operazioni di importazione ed esportazione possono essere combinate per eseguire la migrazione di un'applicazione livello dati tra istanze o per creare un backup logico o per creare una copia on-premise di un database distribuito in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Il processo di esportazione compila un nuovo file di esportazione dell'applicazione livello dati in due fasi.  
  
1.  L'esportazione compila una definizione dell'applicazione livello dati nel file di esportazione (file BACPAC) così come un'operazione di estrazione dell'applicazione livello dati compila una definizione dell'applicazione livello dati in un file del pacchetto di applicazione livello dati. La definizione del pacchetto di applicazione livello dati esportata include tutti gli oggetti del database corrente. Se il processo di esportazione viene eseguito su un database distribuito originariamente da un'applicazione livello dati, e le modifiche sono state apportate direttamente al database dopo la distribuzione, la definizione esportata corrisponderà al set di oggetti del database e non alle definizioni dell'applicazione livello dati originale.  
  
2.  L'esportazione consente di eseguire una copia bulk dei dati da tutte le tabelle del database e di incorporarli nel file di esportazione.  
  
 Il processo di esportazione imposta la versione dell'applicazione livello dati su 1.0.0.0 e la descrizione dell'applicazione livello dati nel file di esportazione su una stringa vuota. Se il database è stato distribuito da un'applicazione livello dati, la definizione dell'applicazione livello dati nel file di esportazione conterrà il nome assegnato all'applicazione livello dati originale, in caso contrario il nome dell'applicazione livello dati verrà impostato sul nome del database.  
  

###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Un database o un'applicazione livello dati può essere esportata solo da un database in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o versioni successive.  
  
 Non è possibile esportare un database contenente oggetti non supportati in un'applicazione livello dati o utenti contenuti. Per ulteriori informazioni sui tipi di oggetti supportati in un'applicazione livello dati, vedere [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 L'esportazione di un'applicazione livello dati richiede almeno le autorizzazioni ALTER ANY LOGIN e VIEW DEFINITION nell'ambito del database, oltre alle autorizzazioni SELECT su **sys.sql_expression_dependencies**. L'esportazione di un'applicazione livello dati può essere effettuata da membri del ruolo predefinito del server securityadmin che sono anche membri del ruolo predefinito del database database_owner nel database dal cui viene esportata l'applicazione livello dati. Possono esportare un'applicazione livello dati anche i membri del ruolo predefinito del server sysadmin o dell'account amministratore di sistema SQL Server predefinito denominato **sa** .  
  
##  <a name="using-the-export-data-tier-application-wizard"></a><a name="UsingDeployDACWizard"></a>Utilizzo della procedura guidata Esporta applicazione livello dati  
 **Per esportare un'applicazione livello dati tramite una procedura guidata**  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], locale o in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  In **Esplora oggetti**espandere il nodo per le istanze da cui esportare l'applicazione livello dati.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del database.  
  
4.  Fare clic su **Attività** e quindi selezionare **Esporta l'applicazione livello dati**.  
  
5.  Completare le finestre di dialogo della procedura guidata.  
  
    -   [Pagina Introduzione](#Introduction)  
  
    -   [Pagina Impostazioni di esportazione](#Export_settings)  
  
    -   [Pagina Convalida](#Validation)  
  
    -   [Pagina Riepilogo](#Summary)  
  
    -   [Pagina Stato](#Progress)  
  
    -   [Pagina Risultati](#Results)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per la procedura guidata Esporta l'applicazione livello dati.  
  
 **Opzioni**  
  
 **Non visualizzare più questa pagina** Selezionare la casella di controllo per evitare che la pagina Introduzione venga visualizzata nuovamente in futuro.  
  
 **Avanti** : consente di passare alla pagina **Selezione pacchetto di applicazione livello dati** .  
  
 **Annulla** : Annulla l'operazione e chiude la procedura guidata.  
  
##  <a name="export-settings-page"></a><a name="Export_settings"></a>Pagina impostazioni di esportazione  
 Utilizzare questa pagina per specificare il percorso in cui creare il file BACPAC.  
  
-   **Salva su disco locale** : crea un file BACPAC in una directory nel computer locale. Fare clic su **Sfoglia** per selezionare un percorso nel computer locale oppure specificare il percorso nell'apposito campo. Il nome del percorso deve includere un nome file e l'estensione .bacpac.  
  
-   **Salva in Azure** : crea un file BACPAC in un contenitore Azure. È necessario connettersi a un contenitore Azure per convalidare questa opzione. Questa opzione richiede inoltre che si specifichi una directory locale per il file temporaneo. Il file temporaneo verrà creato nel percorso specificato, dove vi rimarrà una volta completata l'operazione.  
  
 Per specificare un subset di tabelle da esportare, usare l'opzione **Avanzate** .  
  
##  <a name="validation-page"></a><a name="Validation"></a>Pagina convalida  
 Utilizzare la pagina di convalida per esaminare gli eventuali problemi che bloccano l'operazione. Per continuare, risolvere i problemi che causano il blocco, quindi fare clic su **Ripeti convalida** per assicurarsi che la convalida venga completata correttamente.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="summary-page"></a><a name="Summary"></a> Pagina Riepilogo  
 Utilizzare questa pagina per esaminare le impostazioni di origine e destinazione specificate per l'operazione. Per completare l'operazione di esportazione usando le impostazioni specificate, fare clic su **Fine**. Per annullare l'operazione di esportazione e chiudere la procedura guidata, fare clic su **Annulla**.  
  
##  <a name="progress-page"></a><a name="Progress"></a> Pagina Stato  
 In questa pagina viene visualizzato un indicatore di stato che indica lo stato dell'operazione. Per visualizzare lo stato dettagliato, fare clic sull'opzione **Visualizza dettagli** .  
  
##  <a name="results-page"></a><a name="Results"></a>Pagina dei risultati  
 In questa pagina viene riportato l'esito positivo o negativo dell'operazione di esportazione, indicante i risultati di ogni azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Fare clic sul collegamento per visualizzare un report dell'errore relativo all'azione.  
  
 Fare clic su **fine** per chiudere la procedura guidata.  
  
##  <a name="using-a-net-framework-application"></a><a name="NetApp"></a>Uso di un'applicazione .NET Framework  
 **Per esportare un'applicazione livello dati con il metodo Export() in un'applicazione .NET Framework.**  
  
 Per visualizzare un esempio di codice, scaricare l'applicazione di esempio dell'applicazione livello dati da [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575).  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza contenente l'applicazione livello dati da esportare.  
  
2.  Aprire un oggetto `ServerConnection` e collegarlo alla stessa istanza.  
  
3.  Utilizzare il metodo `Export` del tipo `Microsoft.SqlServer.Management.Dac.DacStore` per esportare l'applicazione livello dati. Specificare il nome dell'applicazione livello dati da esportare e il percorso della cartella in cui salvare il file di esportazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](data-tier-applications.md)   
 [Estrarre un'applicazione livello dati da un database](extract-a-dac-from-a-database.md)  
  
  
