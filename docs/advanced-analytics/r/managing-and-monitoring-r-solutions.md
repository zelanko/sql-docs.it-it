---
title: Gestire e integrare machine learning i carichi di lavoro - SQL Server Machine Learning Services
description: Un amministratore del Server di database SQL, esaminare le attività amministrative per la distribuzione di un sottosistema di R e Python in un'istanza del motore di database di apprendimento.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c9b1b4eca18a9d4d8d1819eee399676046cc9d78
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503829"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Gestire e integrare i carichi di lavoro di machine learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è per gli amministratori di database di SQL Server che sono responsabili della distribuzione di un'infrastruttura di analisi scientifica dei dati efficiente su una risorsa di server che supportano più carichi di lavoro. Delimita l'area dei problemi amministrativi rilevante per la gestione di R e Python codice l'esecuzione in SQL Server. 

## <a name="what-is-feature-integration"></a>Che cos'è l'integrazione delle funzionalità

Apprendimento R e Python viene fornito da [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) come estensione a un'istanza del motore di database. L'integrazione avviene principalmente attraverso il livello di sicurezza e data definition language, riepilogato come segue:

+ Le stored procedure sono dotate in grado di accettare R e Python codice come parametri di input. Gli sviluppatori e data Scientist può usare una [stored procedure di sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) o creare una routine personalizzata che esegue il wrapping del codice.
+ Funzioni T-SQL (vale a dire [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) in grado di usare un modello di dati precedentemente sottoposti a training. Questa funzionalità è disponibile tramite T-SQL. Di conseguenza, può chiamato su un sistema che non dispone di machine learning sono estensioni installate in modo specifico.
+ Account di accesso di database esistenti e le autorizzazioni in base al ruolo riguardano gli script chiamato dall'utente che usano gli stessi dati. Come regola generale, se gli utenti non possono accedere ai dati tramite una query, non possono accedere, tramite lo script sia.

## <a name="feature-availability"></a>Disponibilità delle funzionalità

Integrazione di R e Python diventa disponibile con una successione di questa procedura. Il primo è il programma di installazione, quando si [includere oppure aggiungere i **servizi di Machine Learning** ](../install/sql-machine-learning-services-windows-install.md) funzionalità a un'istanza del motore di database. Come passaggio successivo, è necessario abilitare la creazione di script esterni nell'istanza del motore di database (è per impostazione predefinita).

A questo punto, solo gli amministratori del database dispone dell'autorizzazione completa per creare ed eseguire gli script esterni, aggiungere o eliminare i pacchetti e creare le stored procedure e altri oggetti.

Tutti gli altri utenti devono essere concessa l'autorizzazione EXECUTE ANY EXTERNAL SCRIPT. Ulteriori [autorizzazioni di database standard](../security/user-permission.md) determinare se gli utenti possono creare oggetti, eseguire gli script, utilizzare i modelli serializzati e sottoposto a training e così via. 

## <a name="resource-allocation"></a>Allocazione delle risorse

Stored procedure e query T-SQL che richiamano l'elaborazione esterna è possibile usare le risorse disponibili per il pool di risorse predefinito. Come parte della configurazione predefinita, i processi esterni, ad esempio le sessioni di R e Python sono consentiti fino al 20% della memoria totale nel sistema host. 

Se si desidera adattare sulle risorse, è possibile modificare il pool predefinito, con conseguente effetto sui carichi di lavoro di machine learning in esecuzione in tale sistema.

Un'altra opzione consiste nel creare un pool di risorse esterne personalizzato per acquisire le sessioni provenienti da programmi specifici, gli host o attività che si verificano durante gli intervalli di tempo specifico. Per altre informazioni, vedere [governance delle risorse per modificare i livelli di risorse per l'esecuzione di R e Python](../administration/resource-governance.md) e [come creare un pool di risorse](../administration/how-to-create-a-resource-pool.md) per istruzioni dettagliate.

## <a name="isolation-and-containment"></a>Isolamento e contenimento

L'architettura di elaborazione è progettato per isolare gli script esterni dall'elaborazione del motore di base. Gli script R e Python eseguito come processo separato, in account di lavoro locale. In Gestione attività, è possibile monitorare i processi R e Python, l'esecuzione con un account utente locale con privilegi limitati, distinto dall'account del servizio SQL Server. 

I processi R e Python in esecuzione in account individuali con privilegi limitati presenta i vantaggi seguenti:

+ Isola i processi del motore di core da sessioni di R e Python che è possibile terminare un processo R o Python senza conseguenze per le operazioni del database principale. 

+ Consente di ridurre i privilegi dei processi di runtime dello script esterno nel computer host.

Gli account con privilegi minimi vengono creati durante l'installazione e inseriti in un Windows *pool di account utente* chiamato **SQLRUserGroup**. Per impostazione predefinita, questo gruppo dispone dell'autorizzazione per utilizzare i file eseguibili, librerie e i set di dati incorporati nella cartella del programma per R e Python in SQL Server. 

Come amministratore di database, è possibile utilizzare la protezione dei dati di SQL Server per specificare gli utenti autorizzati a eseguire gli script e che i dati utilizzati nel processi sia gestiti con gli stessi ruoli di sicurezza che consentono di controllare accedere tramite query T-SQL. Come amministratore di sistema, è possibile negare in modo esplicito **SQLRUserGroup** accesso ai dati sensibili nel server locale mediante la creazione degli ACL.

>[!NOTE]
> Per impostazione predefinita, il **SQLRUserGroup** non dispone di un account di accesso o le autorizzazioni in SQL Server. Account di lavoro richiede un account di accesso per l'accesso ai dati, è necessario crearlo manualmente. Uno scenario che chiama in modo specifico per la creazione di un account di accesso deve supportare le richieste provenienti da uno script in esecuzione, per dati o le operazioni nell'istanza del motore di database, quando l'identità dell'utente è un utente di Windows e la stringa di connessione specifica utente attendibile. Per altre informazioni, vedere [aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

## <a name="disable-script-execution"></a>Disabilitare l'esecuzione di script

In caso di script sfuggiti al controllo, è possibile disabilitare tutti l'esecuzione di script, invertendo i passaggi effettuati in precedenza per consentire l'esecuzione di script esterni in primo luogo.

1. In SQL Server Management Studio o un altro strumento di query, eseguire questo comando per impostare `external scripts enabled` su 0 o FALSE.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Riavviare il servizio motore di database.

Dopo aver risolto il problema, ricordare di abilitare di nuovo l'esecuzione di script nell'istanza se si desidera riprendere R e Python scripting supportato nell'istanza del motore di database. Per altre informazioni, vedere [abilitare esecuzione script](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>Estendere le funzionalità

Analisi scientifica dei dati spesso introduce nuovi requisiti per l'amministrazione e distribuzione del pacchetto. Per un data scientist, è pratica comune per sfruttare i pacchetti di terze parti e open source nelle soluzioni personalizzate. Alcuni di questi pacchetti avranno le dipendenze su altri pacchetti, nel qual caso potrebbe essere necessario valutare e installare i pacchetti più per raggiungere l'obiettivo.

Come amministratore di database responsabile di un asset di server, la distribuzione di pacchetti R e Python arbitrari a un server di produzione rappresenta una sfida familiarità. Prima di aggiungere i pacchetti, è necessario stabilire se la funzionalità fornita dal pacchetto esterno è realmente necessaria, con nessun parametro equivalente in integrato [linguaggio R](r-libraries-and-data-types.md) e [librerie Python](../python/python-libraries-and-data-types.md) installato dal programma di installazione SQL Server. 

Come alternativa all'installazione del pacchetto server, potrebbe essere in grado di un data scientist [compilare ed eseguire soluzioni in una workstation esterna](../r/set-up-a-data-science-client.md), il recupero dei dati da SQL Server, ma con tutte le analisi eseguite in locale nella workstation anziché sullo stesso server. 

Se in seguito si determina che le funzioni della libreria esterna sono necessari e non un rischio per operazioni del server o di dati nel suo complesso, è possibile scegliere di metodologie più per aggiungere i pacchetti. Nella maggior parte dei casi, sono necessari diritti di amministratore per aggiungere i pacchetti in SQL Server. Per altre informazioni, vedere [pacchetti di installazione di Python in SQL Server](../python/install-additional-python-packages-on-sql-server.md) e [installare pacchetti R in SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> Per i pacchetti R, diritti di amministratore di server non sono specificamente necessari per l'installazione del pacchetto se si usano metodi alternativi. Visualizzare [installare pacchetti R in SQL Server](install-additional-r-packages-on-sql-server.md) per informazioni dettagliate.

## <a name="monitoring-script-execution"></a>L'esecuzione di script di monitoraggio

Gli script R e Python in esecuzione in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] vengono avviati mediante il [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interfaccia. Tuttavia, Launchpad non viene regolata o monitorato separatamente, perché è un servizio sicuro fornito da Microsoft che gestisce in modo appropriato le risorse della risorsa.

Gli script esterni eseguiti con il servizio Launchpad vengono gestiti mediante il [oggetto processo Windows](/windows/desktop/ProcThread/job-objects). Un oggetto processo consente di gestire gruppi di processi come unità. Ogni oggetto processo è gerarchico e controlla gli attributi di tutti i processi associati a esso. Le operazioni eseguite su un oggetto processo interessano tutti i processi associati all'oggetto processo.

Se quindi è necessario terminare un processo associato a un oggetto, tenere presente che verranno terminati anche tutti i processi correlati. Se si esegue uno script R assegnato a un oggetto processo di Windows e tale script esegue un processo ODBC correlato che deve essere terminato, verrà terminato anche il processo di script R padre.

Se si avvia uno script esterno che utilizza l'elaborazione parallela, un singolo oggetto processo Windows gestisce tutti i processi figlio paralleli.

Per determinare se un processo è in esecuzione in un processo, usare la funzione `IsProcessInJob`.

## <a name="next-steps"></a>Passaggi successivi

+ Rivedere i concetti e componenti del [architettura di estendibilità](../concepts/extensibility-framework.md) e [sicurezza](../concepts/security.md) per altre informazioni di base.

+ Come parte dell'installazione delle funzionalità, potrebbero già avere familiarità con l'utente finale dei dati, controllo di accesso, ma in caso contrario, vedere [concedere le autorizzazioni utente per SQL Server machine Learning Services](../security/user-permission.md) per informazioni dettagliate. 

+ Informazioni su come modificare le risorse di sistema per i carichi di lavoro di apprendimento automatico a elevato utilizzo di calcolo. Per altre informazioni, vedere [come creare un pool di risorse](../administration/how-to-create-a-resource-pool.md).
