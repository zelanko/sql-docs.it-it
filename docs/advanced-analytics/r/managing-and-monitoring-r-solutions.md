---
title: Gestire e integrare i carichi di lavoro di Machine Learning
description: Per SQL Server DBA, rivedere le attività amministrative per la distribuzione di un sottosistema R e Python di Machine Learning in un'istanza del motore di database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fab91e142fad3bcb1ce23816d6705f7a7d208851
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345322"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Gestisci e integra i carichi di lavoro di Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è per gli amministratori di database SQL Server responsabili della distribuzione di un'infrastruttura data science efficiente in un asset server che supporta più carichi di lavoro. Incornicia lo spazio del problema amministrativo pertinente per la gestione dell'esecuzione del codice R e Python in SQL Server. 

## <a name="what-is-feature-integration"></a>Che cos'è l'integrazione delle funzionalità

R e Python Machine Learning sono forniti da [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) come estensione di un'istanza del motore di database. L'integrazione avviene principalmente tramite il livello di sicurezza e la Data Definition Language, riepilogando come segue:

+ Le stored procedure sono dotate della possibilità di accettare codice R e Python come parametri di input. Gli sviluppatori e i data scientist possono usare un [stored procedure di sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) o creare una procedura personalizzata che esegue il wrapping del codice.
+ Funzioni T-SQL (vale a dire, [Predict](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) che possono utilizzare un modello di dati precedentemente sottoposto a training. Questa funzionalità è disponibile tramite T-SQL. Di conseguenza, può essere chiamato in un sistema in cui non sono installate in modo specifico le estensioni di machine learning.
+ Gli account di accesso al database e le autorizzazioni basate sui ruoli esistenti coprono gli script richiamati dall'utente che utilizzano gli stessi dati. Come regola generale, se gli utenti non sono in grado di accedere ai dati tramite una query, non possono accedervi tramite uno script.

## <a name="feature-availability"></a>Disponibilità delle funzionalità

L'integrazione di R e Python diventa disponibile con una serie di passaggi. Il primo è il programma di installazione, quando si [include o si aggiunge la funzionalità **Machine Learning Services** ](../install/sql-machine-learning-services-windows-install.md) a un'istanza del motore di database. Come passaggio successivo, è necessario abilitare l'esecuzione di script esterni nell'istanza del motore di database (è disattivata per impostazione predefinita).

A questo punto, solo gli amministratori di database hanno l'autorizzazione completa per creare ed eseguire script esterni, aggiungere o eliminare pacchetti, nonché creare stored procedure e altri oggetti.

A tutti gli altri utenti deve essere concessa l'autorizzazione EXECUTE ANY EXTERNAL SCRIPT. Ulteriori [autorizzazioni di database standard](../security/user-permission.md) determinano se gli utenti possono creare oggetti, eseguire script, utilizzare modelli serializzati e sottoposti a training e così via. 

## <a name="resource-allocation"></a>Allocazione delle risorse

Le stored procedure e le query T-SQL che richiamano l'elaborazione esterna utilizzano le risorse disponibili per il pool di risorse predefinito. Come parte della configurazione predefinita, i processi esterni come le sessioni R e Python sono consentiti fino al 20% della memoria totale nel sistema host. 

Se si vuole modificare nuovamente la resourcing, è possibile modificare il pool predefinito, con l'effetto corrispondente sui carichi di lavoro di Machine Learning in esecuzione nel sistema.

Un'altra opzione consiste nel creare un pool di risorse esterne personalizzato per acquisire sessioni provenienti da programmi, host o attività specifici che si verificano durante intervalli di tempo specifici. Per altre informazioni, vedere [governance delle risorse per modificare i livelli di risorse per l'esecuzione di R e Python](../administration/resource-governance.md) e [come creare un pool di risorse](../administration/how-to-create-a-resource-pool.md) per istruzioni dettagliate.

## <a name="isolation-and-containment"></a>Isolamento e contenimento

L'architettura di elaborazione è progettata per isolare gli script esterni dall'elaborazione principale del motore. Gli script R e Python vengono eseguiti come processi distinti in account di lavoro locali. In Gestione attività è possibile monitorare i processi R e Python, in esecuzione con un account utente locale con privilegi di basso livello, distinti dall'account del servizio SQL Server. 

L'esecuzione di processi R e Python nei singoli account con privilegi limitati presenta i vantaggi seguenti:

+ Isola i processi del motore di base da sessioni R e Python è possibile terminare un processo R o Python senza influito sulle operazioni di base del database. 

+ Riduce i privilegi dei processi di runtime di script esterni nel computer host.

Gli account con privilegi minimi vengono creati durante l'installazione e inseriti in un *pool di account utente* di Windows denominato **SQLRUserGroup**. Per impostazione predefinita, questo gruppo dispone dell'autorizzazione per l'utilizzo di file eseguibili, librerie e set di impostazioni predefiniti nella cartella Program per R e Python in SQL Server. 

In qualità di amministratore di database, è possibile utilizzare SQL Server sicurezza dei dati per specificare chi dispone dell'autorizzazione per l'esecuzione di script e che i dati utilizzati nei processi vengono gestiti con gli stessi ruoli di sicurezza che controllano l'accesso tramite query T-SQL. Come amministratore di sistema, è possibile negare in modo esplicito l'accesso **SQLRUserGroup** ai dati sensibili nel server locale creando ACL.

>[!NOTE]
> Per impostazione predefinita, **SQLRUserGroup** non dispone di un account di accesso o di autorizzazioni nel SQL Server stesso. Se gli account di lavoro richiedono un account di accesso per l'accesso ai dati, è necessario crearlo manualmente. Uno scenario che chiama specificamente per la creazione di un account di accesso è supportare le richieste da uno script in esecuzione, per i dati o le operazioni nell'istanza del motore di database, quando l'identità utente è un utente di Windows e la stringa di connessione specifica un utente attendibile. Per altre informazioni, vedere [aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="disable-script-execution"></a>Disabilitare l'esecuzione di script

In caso di script di Runaway, è possibile disabilitare l'esecuzione di tutti gli script, invertendo i passaggi precedentemente eseguiti per consentire l'esecuzione di script esterni in primo luogo.

1. In SQL Server Management Studio o in un altro strumento di query eseguire questo comando `external scripts enabled` per impostare su 0 o su false.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Riavviare il servizio motore di database.

Una volta risolto il problema, ricordarsi di riabilitare l'esecuzione di script nell'istanza se si desidera riprendere il supporto di script R e Python nell'istanza del motore di database. Per altre informazioni, vedere [abilitare l'esecuzione di script](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>Estendi funzionalità

Data Science introduce spesso nuovi requisiti per la distribuzione e l'amministrazione dei pacchetti. Per i data scientist è prassi comune sfruttare i pacchetti open source e di terze parti nelle soluzioni personalizzate. Alcuni di questi pacchetti avranno dipendenze da altri pacchetti, nel qual caso potrebbe essere necessario valutare e installare più pacchetti per raggiungere l'obiettivo.

In qualità di amministratore di database responsabile di un asset server, la distribuzione di pacchetti R e Python arbitrari su un server di produzione rappresenta una sfida non familiare. Prima di aggiungere i pacchetti, è necessario valutare se la funzionalità fornita dal pacchetto esterno è effettivamente richiesta, senza equivalenti nel [linguaggio R](r-libraries-and-data-types.md) incorporato e nelle [librerie Python](../python/python-libraries-and-data-types.md) installate dal programma di installazione di SQL Server. 

In alternativa all'installazione di un pacchetto server, un data scientist potrebbe essere in grado di [compilare ed eseguire soluzioni su una workstation esterna](../r/set-up-a-data-science-client.md), recuperando i dati da SQL Server, ma con tutte le analisi eseguite localmente nella workstation anziché nel server stesso. 

Se successivamente si determina che le funzioni della libreria esterna sono necessarie e non si costituisce un rischio per le operazioni del server o i dati nel suo complesso, è possibile scegliere tra più metodologie per aggiungere pacchetti. Nella maggior parte dei casi, è necessario disporre dei diritti di amministratore per aggiungere pacchetti a SQL Server. Per altre informazioni, vedere [Install Python Packages in SQL Server](../python/install-additional-python-packages-on-sql-server.md) e [Install R packages in SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> Per i pacchetti R, i diritti di amministratore del server non sono specificamente necessari per l'installazione del pacchetto se si usano metodi alternativi. Per informazioni dettagliate, vedere [Install R packages in SQL Server](install-additional-r-packages-on-sql-server.md) .

## <a name="monitoring-script-execution"></a>Monitoraggio dell'esecuzione di script

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Gli[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] script R e Python eseguiti in vengono avviati dall'interfaccia. Tuttavia, la finestra di avvio non è gestita o monitorata separatamente, poiché si tratta di un servizio sicuro fornito da Microsoft che gestisce le risorse in modo appropriato.

Gli script esterni eseguiti con il servizio Launchpad vengono gestiti mediante l' [oggetto processo di Windows](/windows/desktop/ProcThread/job-objects). Un oggetto processo consente di gestire gruppi di processi come unità. Ogni oggetto processo è gerarchico e controlla gli attributi di tutti i processi associati a esso. Le operazioni eseguite su un oggetto processo interessano tutti i processi associati all'oggetto processo.

Se quindi è necessario terminare un processo associato a un oggetto, tenere presente che verranno terminati anche tutti i processi correlati. Se si esegue uno script R assegnato a un oggetto processo di Windows e tale script esegue un processo ODBC correlato che deve essere terminato, verrà terminato anche il processo di script R padre.

Se si avvia uno script esterno che utilizza l'elaborazione parallela, un singolo oggetto processo di Windows gestisce tutti i processi figlio paralleli.

Per determinare se un processo è in esecuzione in un processo, usare la funzione `IsProcessInJob`.

## <a name="next-steps"></a>Passaggi successivi

+ Esaminare i concetti e i componenti dell' [architettura](../concepts/extensibility-framework.md) di estendibilità e la [sicurezza](../concepts/security.md) per ulteriori informazioni di base.

+ Come parte dell'installazione di funzionalità, è possibile che si abbia già familiarità con il controllo di accesso ai dati dell'utente finale, ma in caso contrario, vedere [concedere le autorizzazioni utente per SQL Server machine learning](../security/user-permission.md) per informazioni dettagliate. 

+ Informazioni su come modificare le risorse di sistema per carichi di lavoro di apprendimento automatico a elevato utilizzo di calcolo. Per ulteriori informazioni, vedere [come creare un pool di risorse](../administration/how-to-create-a-resource-pool.md).
