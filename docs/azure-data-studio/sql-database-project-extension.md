---
title: Estensione progetti di database SQL
description: Installare e usare l'estensione progetti di database SQL (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 07/30/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 39ebf2d26e69e47edc700a489743d70762bef7b0
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88199985"
---
# <a name="sql-database-projects-extension-preview"></a>Estensione progetti di database SQL (anteprima)

L'estensione progetti di database SQL (anteprima) è un'estensione per lo sviluppo di database SQL in un ambiente di sviluppo basato su progetto. Questa estensione, attualmente in anteprima, è disponibile nella [build per utenti Insiders di Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).


## <a name="features"></a>Funzionalità
1. Creare un progetto da un database connesso 
2. Creare un nuovo progetto vuoto
3. Aprire un progetto creato in precedenza in [Azure Data Studio](sql-database-project-extension-getting-started.md) o in [SQL Server Data Tools](../ssdt/sql-server-data-tools.md) 
4. Modificare il progetto aggiungendo o rimuovendo una tabella, una vista, una stored procedure o script personalizzati nel progetto 
5. Organizzare file/script in cartelle 
6. Aggiungere riferimenti a database di sistema o al file DACPAC utente
7. Compilare un progetto singolo 
8. Distribuire un progetto singolo
9. Caricare i dettagli della connessione (autenticazione di Windows per SQL) e le variabili di SQLCMD dal profilo di distribuzione 

## <a name="install-the-sql-database-projects-extension"></a>Installare l'estensione progetti di database SQL

1. Aprire Gestione estensioni per accedere alle estensioni disponibili.  A questo scopo, selezionare l'icona delle estensioni o selezionare **Estensioni** dal menu **Visualizza**.
2. Identificare l'estensione *progetti di database SQL* digitandone il nome, per intero o in parte, nella casella di ricerca delle estensioni. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![Installare l'estensione](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. Selezionare l'estensione desiderata e **installarla**.
4. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).
5. Selezionare l'icona File dalla barra attività oppure selezionare **Explorer** dal menu **Visualizza**. È ora disponibile un nuovo viewlet per **Progetti**.


   > [!NOTE]
   > .NET Core SDK è necessario per la funzionalità di compilazione del progetto e verrà richiesta l'installazione di .NET Core SDK se non viene rilevato dall'estensione.  È possibile scaricare e installare .NET Core SDK (v3.1 o versione successiva) da [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1).

   > [!NOTE]
   > Per usufruire della funzionalità completa, insieme all'estensione progetti di database SQL è consigliabile installare l'[estensione confronto schemi](schema-compare-extension.md).

## <a name="known-limitations"></a>Limitazioni note
1. L'aggiunta di riferimenti a progetti e il caricamento di riferimenti a progetti esistenti nel viewlet di Azure Data Studio non sono attualmente supportati. 
2. Il caricamento dei file come collegamento non è attualmente supportato nel viewlet di Azure Data Studio, ma i file verranno caricati nel livello principale dell'albero e la compilazione incorporerà questi file come previsto. 
3. L'aggiunta e il caricamento di script nel viewlet prima e dopo la distribuzione non sono attualmente supportati, ma se i file vengono aggiunti manualmente nel progetto, verranno presi in considerazione in fase di compilazione. 
3. Gli oggetti SQLCLR nel progetto non sono supportati nella versione .NET Core di DacFx. 
3. Le attività (compilazione/pubblicazione) non sono definite dall'utente
3. Destinazioni di pubblicazioni definite da DacFx
3. L'integrazione del controllo del codice sorgente e la creazione di nuovi progetti non creano automaticamente un file con estensione gitignore 
3. Il supporto per l'ambiente WSL è limitato 

## <a name="next-steps"></a>Passaggi successivi
- [Introduzione all'estensione progetti di database SQL](sql-database-project-extension-getting-started.md)
- [Compilare e pubblicare un progetto con l'estensione progetti di database SQL per Azure Data Studio](sql-database-project-extension-build.md)