---
title: Origine Power Query | Microsoft Docs
description: Informazioni su come configurare l'origine Power Query nel flusso di dati di SQL Server Integration Services
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.powerqueryconnmgr.f1
- sql13.ssis.designer.powerquerysource.queries.f1
- sql13.ssis.designer.powerquerysource.connmgrs.f1
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: efefe16b7c5180ed0ae0dd853737c2182f335f61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034400"
---
# <a name="power-query-source-preview"></a>Origine Power Query (anteprima)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Questo articolo descrive come configurare le proprietà dell'origine Power Query nel flusso di dati di SQL Server Integration Services (SSIS). Power Query è una tecnologia che consente di connettersi a diverse origini dati e trasformare dati tramite Excel o Power BI Desktop. Per altre informazioni, vedere l'articolo [Panoramica e formazione su Power Query](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d). Lo script generato da Power Query può essere copiato e incollato nell'origine Power Query nel flusso di dati SSIS per configurarlo.
  
> [!NOTE]
> Per la versione di anteprima corrente, per facilitare la raccolta rapida di commenti e suggerimenti oltre all'introduzione di miglioramenti frequenti per le funzionalità, l'origine Power Query può essere usata solo in SQL Server Data Tools (SSDT) e Azure-SSIS Integration Runtime (IR) in Azure Data Factory (ADF). È possibile scaricare l'ultima versione di SSDT che supporta l'origine Power Query da [qui](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017). Per eseguire il provisioning di Azure-SSIS IR, vedere l'articolo [Eseguire il provisioning del runtime di integrazione SSIS di Azure in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="configure-the-power-query-source"></a>Configurare l'origine Power Query

Per aprire l'**editor dell'origine Power Query** in SSDT, trascinare **Origine Power Query** dalla casella degli strumenti di SSIS nella finestra di progettazione del flusso di dati e fare doppio clic su di esso.  

![Origine PQ](media/power-query-source/pq-source.png)

Sul lato sinistro vengono visualizzate tre schede. Nella scheda **Queries** (Query) è possibile selezionare la modalità di query nell'elenco a discesa.
-   La modalità **Single Query** (Query singola) consente di copiare e incollare un singolo script di Power Query da Excel o Power BI Desktop.
-   La modalità **Single Query from Variable** (Query singola da variabile) consente di specificare una variabile stringa che contiene la query da eseguire.

![Scheda Queries (Query) origine PQ](media/power-query-source/pq-source-queries-tab-single.png)

Nella scheda **Connection Managers** (Gestioni connessioni) è possibile aggiungere o rimuovere le gestioni connessioni di Power Query che contengono credenziali di accesso all'origine dati. Selezionando il pulsante **Detect Data Source** (Rileva origine dati) vengono identificate ed elencate le origini dati di riferimento nella query, in modo da poter assegnare le gestioni connessioni di Power Query esistenti appropriate oppure di crearne di nuove.

![Rilevamento, scheda Connection Managers (Gestioni connessioni) origine PQ](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![Aggiunta, scheda Connection Managers (Gestioni connessioni) origine PQ](media/power-query-source/pq-source-connection-managers-tab-add.png)

Infine, nella scheda **Columns** (Colonne) è possibile modificare le informazioni sulle colonne di output.

![Scheda Columns (Colonne) origine PQ](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>Configurare la gestione connessione di Power Query

Quando si progetta il flusso di dati con l'origine Power Query in SSDT, è possibile creare una nuova gestione connessione di Power Query nei modi seguenti:
- Crearla indirettamente nella scheda **Connection Managers** (Gestioni connessioni) dell'origine Power Query dopo aver selezionato il pulsante **Add**/**Detect Data Source** (Aggiungi > Rileva origine dati) e selezionando **<New connection...>** nell'elenco a discesa come descritto in precedenza.
- Crearla direttamente facendo clic con il pulsante destro del mouse sul pannello **Gestioni connessioni** del pacchetto e scegliendo **Nuova connessione** dal menu a discesa.

![Aggiunta, pannello Gestioni connessioni origine PQ](media/power-query-source/pq-source-connection-managers-panel-add.png)

Nella finestra di dialogo **Aggiungi gestione connessione SSIS** fare doppio clic su **PowerQuery** nell'elenco dei tipi di gestione connessione.

![Finestra di dialogo Aggiungi gestione connessione SSIS origine PQ](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

Nell'**Editor gestione connessione Power Query** è necessario specificare **Data Source Kind** (Tipo origine dati), **Data Source Path** (Percorso origine dati) e **Authentication Kind** (Tipo di autenticazione), oltre ad assegnare le credenziali di accesso appropriate. Per **Data Source Kind** (Tipo origine dati) è attualmente possibile selezionare uno dei 22 tipi nel menu a discesa.

![Tipo, Editor gestione connessione origine PQ](media/power-query-source/pq-source-connection-manager-editor-kind.png)

Alcune di queste origini (**Oracle**, **DB2**, **MySQL**, **PostgreSQL**, **Teradata**, **Sybase**) richiedono ulteriori installazioni di driver ADO.NET che possono essere ottenuti dall'articolo [Prerequisiti delle origini dati (Power Query)](https://support.office.com/article/data-source-prerequisites-power-query-6062cf52-c764-45d0-a1c6-fbf8fc05b05a). È possibile usare l'interfaccia di installazione personalizzata per installarli in Azure-SSIS IR. Vedere l'articolo [Personalizzare l'installazione del runtime di integrazione Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

Per **Data Source Path** (Percorso origine dati), è possibile immettere le proprietà specifiche dell'origine dati che costituiscono una stringa di connessione senza le informazioni di autenticazione. Ad esempio, il percorso per l'origine dati **SQL** viene composto come `<Server>;<Database>`. È possibile selezionare il pulsante **Edit** (Modifica) per assegnare valori alle proprietà specifiche dell'origine dati che compongono il percorso.

![Percorso, Editor gestione connessione origine PQ](media/power-query-source/pq-source-connection-manager-editor-path.png)

Infine, per **Authentication Kind** (Tipo di autenticazione), è possibile selezionare **Anonymous**/**Windows Authentication**/**Username Password**/**Key** (Anonima, Autenticazione di Windows, Nome utente, Password, Chiave) nel menu a discesa, immettere le credenziali di accesso appropriate e selezionare il pulsante **Test Connection** (Test connessione) per assicurarsi che l'origine Power Query sia stata configurata correttamente.

![Autenticazione, Editor gestione connessione origine PQ](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

### <a name="current-limitations"></a>Limitazioni correnti

-   Non è attualmente possibile usare l'origine dati **Oracle** perché il driver Oracle ADO.NET non può essere installato in Azure-SSIS IR. Per il momento, quindi, installare il driver ODBC Oracle e usare l'origine dati **ODBC** per connettersi a Oracle. Vedere l'esempio **ORACLE STANDARD ODBC** nell'articolo [Personalizzare l'installazione del runtime di integrazione Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

-   Non è attualmente possibile usare l'origine dati **Web** in Azure-SSIS IR con una configurazione personalizzata. Per il momento quindi, usare l'origine dati Azure-SSIS IR senza configurazione personalizzata.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come eseguire pacchetti SSIS in Azure-SSIS IR come attività di prima classe nelle pipeline di Azure Data Factory. Vedere l'articolo [Eseguire un pacchetto SSIS tramite l'attività di esecuzione del pacchetto SSIS in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).
