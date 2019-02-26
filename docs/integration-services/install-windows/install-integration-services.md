---
title: Installare SQL Server Integration Services (SSIS) | Microsoft Docs
description: Informazioni su come installare Microsoft SQL Server Integration Services (SSIS) e su come ottenere altri download per SSIS
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9183daa6e11e015bf484002fcf5857adab0ec087
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2019
ms.locfileid: "56801975"
---
# <a name="install-integration-services"></a>Installazione di Integration Services

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di un singolo programma di installazione che consente di installare uno o tutti i componenti, incluso [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Usare il programma di installazione per installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con o senza gli altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un singolo computer.    
    
 Questo articolo include considerazioni importanti di cui tenere conto prima di installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Le informazioni incluse in questo articolo consentono di valutare le opzioni di installazione per effettuare le selezioni appropriate ai fini di una corretta installazione.    
    
## <a name="get-ready-to-install-integration-services"></a>Preparativi per l'installazione di Integration Services    
 Prima di installare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], rivedere le informazioni seguenti:    
    
-   [Requisiti hardware e software per l'installazione di SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="install-standalone-or-side-by-side"></a>Eseguire un'installazione autonoma o affiancata    
È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nelle configurazioni seguenti:    
    
-   È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un computer in cui non sono presenti istanze precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
-   È possibile effettuare un'installazione side-by-side di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e di un'istanza esistente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
    
Quando esegue l'aggiornamento alla versione più recente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un computer con una versione precedente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] già installata, la versione corrente viene installata side-by-side con la versione precedente.    
    
Per altre informazioni sull'aggiornamento di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Aggiornare Integration Services](../../integration-services/install-windows/upgrade-integration-services.md).

## <a name="get-sql-server-with-integration-services"></a>Ottenere SQL Server with Integration Services

Se Microsoft SQL Server non è già disponibile, scaricare una versione di valutazione gratuita, o l'edizione Developer gratuita, dai [download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). SSIS non è incluso nell'edizione Express di SQL Server.

## <a name="install-integration-services"></a>Installazione di Integration Services    
 Dopo avere esaminato i requisiti di installazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e avere verificato che il computer in uso soddisfi tali requisiti, è possibile installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
     
Se per installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] si usa l'Installazione guidata, viene visualizzata una serie di pagine in cui specificare le opzioni e i componenti desiderati.

-   Nella pagina **Selezione funzionalità**, in **Funzionalità condivise**, selezionare **Integration Services**.

-   Facoltativamente, in **Funzionalità istanza** selezionare **Servizi motore di database** per ospitare il database del catalogo SSIS, `SSISDB`, per archiviare, gestire, eseguire e monitorare i pacchetti SSIS.

-   Per installare assembly gestiti per la programmazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], in **Funzionalità condivise** selezionare anche **SDK di strumenti client**.

> [!NOTE]
> Alcuni componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile selezionare per l'installazione nella pagina **Selezione funzionalità** dell'Installazione guidata consentono di installare solo un subset parziale dei componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Tali componenti sono utili per attività specifiche, ma le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] risultano limitate. L'opzione **Servizi Motore di database** , ad esempio, consente di installare i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessari per l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per garantire l'installazione completa di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario selezionare **Integration Services** nella pagina **Selezione funzionalità** .

### <a name="installing-a-dedicated-server-for-etl-processes"></a>Installazione di un server dedicato per i processi ETL

Per usare un server dedicato per i processi di estrazione, trasformazione e caricamento (ETL, Extraction, Transformation and Loading), installare un'istanza locale del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] quando si installa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] i pacchetti vengono in genere archiviati in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e la pianificazione di tali pacchetti si basa su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se il server ETL non è dotato di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], è necessario pianificare o eseguire i pacchetti da un server dotato di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. I pacchetti, di conseguenza, non vengono eseguiti nel server ETL, ma nel server dal quale vengono avviati. Di conseguenza, le risorse del server ETL dedicato non vengono utilizzate come previsto. Inoltre, le risorse di altri server possono essere violate dai processi ETL in esecuzione.

### <a name="configuring-ssis-event-logging"></a>Configurazione della registrazione eventi SSIS
    
Per impostazione predefinita, in una nuova installazione, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene configurato in modo da non registrare gli eventi correlati all'esecuzione dei pacchetti nel registro eventi delle applicazioni. Questa impostazione impedisce la creazione di un numero eccessivo di voci nel registro eventi quando si utilizza la funzionalità di raccolta dati di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Gli eventi non registrati includono EventID 12288, che indica che il pacchetto è stato avviato ed EventID 12289 che indica che il pacchetto è stato completato. Per inserire questi due eventi nel registro eventi dell'applicazione, aprire il Registro di sistema per la modifica. Nel Registro di sistema individuare il nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS e modificare il valore di DWORD dell'impostazione LogPackageExecutionToEventLog da 0 a 1.    
    
## <a name="install-additional-components-for-integration-services"></a>Installare i componenti aggiuntivi per Integration Services

Per un'installazione completa di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], selezionare i componenti necessari dall'elenco seguente:

-   **Integration Services (SSIS)**. Installare SSIS con l'Installazione guidata di SQL Server. Se si seleziona SSIS viene installato quanto segue:

    -   Supporto per il catalogo SSIS nel motore di database di SQL Server.

    -   Facoltativamente, funzionalità SSIS Scale Out, costituita da un master e da diversi ruoli di lavoro.

    -   Componenti SSIS a 32 e a 64 bit.

    -   L'installazione di SSIS **non** installa gli strumenti necessari per progettare e sviluppare pacchetti SSIS.

-   **Motore di database di SQL Server**. Installare il motore di database con l'Installazione guidata di SQL Server. La selezione del motore di database consente di creare e ospitare il database del catalogo SSIS, `SSISDB`, per archiviare, gestire, eseguire e monitorare i pacchetti SSIS.

-   **SQL Server Data Tools (SSDT)**. Per scaricare e installare SSDT, vedere [Scaricare SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md). L'installazione di SSDT consente di progettare e distribuire pacchetti SSIS. Con SSDT vengono installati i componenti seguenti:

    -   Strumenti di progettazione e sviluppo di pacchetti SSIS, incluso Progettazione SSIS.

    -   Solo componenti di SSIS a 32 bit.

    -   Una versione limitata di Visual Studio, se non è installata alcuna edizione di Visual Studio.

    -   Visual Studio Tools for Applications (VSTA), l'editor di script usato dall'attività Script SSIS e dal componente script.

    -   Procedure guidate SSIS tra cui la Distribuzione guidata e l'Aggiornamento guidato pacchetti.

    -   Importazione ed esportazione guidate di SQL Server.

-   **Integration Services Feature Pack per Azure**. Per scaricare e installare il Feature Pack, vedere [Microsoft SQL Server 2017 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=54798). L'installazione del Feature Pack consente la connessione dei pacchetti ai servizi di archiviazione e analisi nel cloud di Azure, inclusi i servizi seguenti:

    -   Archiviazione BLOB di Azure.

    -   Azure HDInsight.

    -   Azure Data Lake Store.

    -   Azure SQL Data Warehouse.

-   **Componenti aggiuntivi facoltativi**. Facoltativamente, da SQL Server Feature Pack è possibile scaricare componenti aggiuntivi di terze parti.

    -   Microsoft® Connector for SAP BW per Microsoft SQL Server®. Per ottenere questi componenti, vedere [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

    -   Connettore Microsoft per Oracle di Attunity versione 5.0 e connettore Teradata Microsoft di Attunity versione 5.0. Per ottenere questi componenti, vedere [Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179) (Connettori Microsoft versione 5.0 per Oracle e Teradata).
