---
title: Estensione progetti di database SQL
description: Installare e usare l'estensione progetti di database SQL (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519170"
---
# <a name="sql-database-projects-extension-preview"></a>Estensione progetti di database SQL (anteprima)

L'estensione progetti di database SQL (anteprima) è un'estensione per lo sviluppo di database SQL in un ambiente di sviluppo basato su progetto. Questa estensione, attualmente in anteprima, è disponibile nella [build per utenti Insiders di Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).


## <a name="install-the-sql-database-projects-extension"></a>Installare l'estensione progetti di database SQL

1. Per aprire Gestione estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni oppure l'opzione **Estensioni** dal menu **Visualizza**.
2. Identificare l'estensione *progetti di database SQL* digitandone il nome, per intero o in parte, nella casella di ricerca delle estensioni. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![Installare l'estensione](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. Selezionare l'estensione desiderata e **installarla**.
4. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).
5. Selezionare l'icona File dalla barra attività oppure selezionare **Explorer** dal menu **Visualizza**. È ora disponibile un nuovo viewlet per **Progetti**.

   > [!NOTE]
   > Per usufruire della funzionalità completa, insieme all'estensione progetti di database SQL è consigliabile installare l'[estensione confronto schemi](schema-compare-extension.md).

## <a name="getting-started-with-database-projects"></a>Introduzione ai progetti di database

* Per creare un nuovo progetto di database, passare al viewlet **Progetti** in Explorer o cercare **Nuovo Progetto di database** nel riquadro comandi.
* È possibile aprire progetti di database esistenti tramite **Apri Progetto di database** nel riquadro comandi.
* Iniziare da un database esistente usando **Importa nuovo progetto di database** dal riquadro comandi.

   ![Nuovo viewlet](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>Creare un progetto di database vuoto

 Nel viewlet **Progetti**in **Explorer** fare clic sul pulsante **Nuovo progetto** e immettere il nome del progetto nella casella di testo di input visualizzata.  Nella finestra di dialogo "Selezionare una cartella" visualizzata selezionare una directory in cui inserire la cartella del progetto, il file con estensione sqlproj e gli altri contenuti.
Il progetto vuoto verrà aperto e visualizzato nel viewlet **Progetti** per la modifica.

### <a name="open-an-existing-project"></a>Aprire un progetto esistente

Nel viewlet **Progetti** fare clic sul pulsante **Apri progetto** e aprire un file con estensione *sqlproj* esistente dall'elemento di selezione file visualizzato. I progetti esistenti possono avere origine da Azure Data Studio o da [Visual Studio SQL Server Data Tools](../ssdt/sql-server-data-tools.md).

Il progetto esistente verrà aperto e il suo contenuto verrà visualizzato nel viewlet **Progetti** per la modifica.

### <a name="create-a-database-project-from-an-existing-database"></a>Creare un progetto di database da un database esistente

Nel viewlet **Progetti** fare clic sul pulsante **Import Project from Database** (Importa progetto da database) e connettersi a SQL Server.  Dopo che la connessione è stata stabilita, selezionare un database dall'elenco dei database disponibili e impostare il nome del progetto.

Selezionare infine una struttura di destinazione dell'estrazione.  Verrà aperto il nuovo progetto, che conterrà gli script SQL per i contenuti del database selezionato.

## <a name="build-and-publish"></a>Compilare e pubblicare

La distribuzione del progetto di database viene eseguita nell'estensione progetti di database SQL per Azure Data Studio tramite la compilazione del progetto in un [file dell'applicazione livello dati ](../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC) e la pubblicazione in una piattaforma supportata. Per altre informazioni su questo processo, vedere [Compilare e pubblicare un progetto](sql-database-project-extension-build.md).

## <a name="schema-compare"></a>Confronto schema
L'estensione progetti di database SQL interagisce con l'[estensione confronto schemi](schema-compare-extension.md), se installata, per confrontare i contenuti di un progetto con un pacchetto di applicazione livello dati o con un database esistente.  Il confronto degli schemi risultante può essere usato per visualizzare e applicare le differenze dall'origine alla destinazione.

## <a name="next-steps"></a>Passaggi successivi

- [Compilare e pubblicare un progetto con l'estensione progetti di database SQL per Azure Data Studio](sql-database-project-extension-build.md)
- [Applicazioni livello dati](../relational-databases/data-tier-applications/data-tier-applications.md)