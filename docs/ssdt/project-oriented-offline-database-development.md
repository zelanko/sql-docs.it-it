---
title: Sviluppo di database offline orientato ai progetti
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.general
- sql.data.tools.dbprojectwizard.summary
ms.assetid: e61e830d-9fcd-45e7-b7b4-93a42155dd56
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 395465b9f07c9927a2a0ed1a277cde9f9e37f587
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243741"
---
# <a name="project-oriented-offline-database-development"></a>Sviluppo di database offline orientato ai progetti

Questa sezione descrive le funzionalità fornite SQL Server Data Tools (SSDT) per la creazione, la compilazione, il debug e la pubblicazione di un progetto di database.  
  
Se si usa SSDT, sarà possibile creare un database di sviluppo da un database di produzione esistente, mentre il team di sviluppo potrà creare un progetto di database offline e implementare modifiche allo schema aggiungendo, modificando o eliminando le definizioni di oggetti (rappresentati da script) nel progetto, senza una connessione a un'istanza del server. Tutte queste operazioni possono essere completate usando Progettazione tabelle o l'editor Transact\-SQL. Inoltre, è possibile scrivere ed eseguire il debug di oggetti Transact\-SQL e CLR nello stesso progetto. È possibile utilizzare Confronto schema per garantire la sincronizzazione tra il progetto e il database di produzione e per creare snapshot per il progetto in ogni fase del ciclo di sviluppo ai fini del confronto. Mentre si lavora sui progetti di database in un ambiente basato su team, è possibile utilizzare il controllo della versione per tutti i file. Al termine dello sviluppo, del test e del debug del progetto di database, è possibile passare il progetto a persone autorizzate affinché venga pubblicato in un ambiente di produzione.  
  
> [!NOTE]  
> Negli argomenti in cui sono descritte le procedure inclusi in questa sezione è contenuta una serie di attività che può essere completata in una sequenza.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|---------|---------------|  
|[Eseguire l'importazione in un progetto di database](../ssdt/import-into-a-database-project.md)|Viene descritta l'importazione di oggetti da un database attivo, un file con estensione dacpac o uno script.|  
|[Finestra di dialogo Aggiungi riferimento al database](../ssdt/add-database-reference-dialog-box.md)|Descrive diversi modi per aggiungere un riferimento a database.|  
|[Finestra di dialogo Controlla aggiornamenti](../ssdt/check-for-updates-dialog-box.md)|Descrive come SQL Server Data Tools può verificare la disponibilità di aggiornamenti di prodotto.|  
|[Impostazioni del progetto di database](../ssdt/database-project-settings.md)|Vengono descritte differenti impostazioni di progetto per controllare gli aspetti del database e le configurazioni di compilazione.|  
|[Procedura: Cercare oggetti in un progetto di database di SQL Server](../ssdt/how-to-browse-objects-in-a-sql-server-database-project.md)|Esplora oggetti di SQL Server in Visual Studio contiene ora un nodo Progetti dedicato, sotto il quale tutti i progetti di database di SQL Server di una soluzione vengono raggruppati in una gerarchia in stile SQL Server Management Studio.|  
|[Finestra Operazioni degli strumenti dati](../ssdt/data-tools-operations-window.md)|Viene descritta la finestra **Operazioni degli strumenti dati** in cui viene visualizzato lo stato di alcune operazioni e vengono notificati eventuali errori.|  
|[Opzioni dell'editor Transact-SQL](../ssdt/transact-sql-editor-options.md)|Descrive le opzioni Transact\-SQL.|  
|[Procedura: Creare un nuovo progetto di database](../ssdt/how-to-create-a-new-database-project.md)|Creare un progetto di database e importare lo schema del database esistente.|  
|[Procedura: Usare il confronto schema per confrontare definizioni di database diverse](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)|Confrontare gli schemi di un database e di un progetto ed eseguirne la sincronizzazione.|  
|[Procedura: Compilare e distribuire in un database locale](../ssdt/how-to-build-and-deploy-to-a-local-database.md)|Usare l'istanza di SQL Server su richiesta locale, che viene attivata quando si esegue il debug di un progetto di database.|  
|[Procedura: Modificare la piattaforma di destinazione e pubblicare un progetto di database](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)|Impostare la piattaforma SQL Server di destinazione per il progetto su qualsiasi istanza supportata di SQL Server e convalidare la sintassi.|  
|[Procedura: Creare uno snapshot di un progetto](../ssdt/how-to-create-a-snapshot-of-a-project.md)|Creare un proxy di sola lettura dello schema del database e ripristinare il progetto di origine qualora vengano applicate al progetto modifiche non desiderate.|  
|[Procedura: Usare oggetti di Microsoft SQL Server 2012 nel progetto](../ssdt/how-to-use-microsoft-sql-server-2012-objects-in-your-project.md)|Aggiungere un nuovo oggetto Sequence al progetto.|  
|[Procedura: Utilizzare oggetti di database CLR](../ssdt/how-to-work-with-clr-database-objects.md)|Creare e pubblicare oggetti CLR nel progetto di database di SQL Server Data Tools.|  
|[Procedura: Convertire progetti di database Visual Studio 2010 in progetti di database di SQL Server e destinarli di nuovo a una piattaforma differente](../ssdt/how-to-convert-visual-studio-2010-database-projects-to-ssql-server-projects.md)|Convertire progetti di database di SQL Server, CLR e di applicazione di livello dati esistenti creati in Visual Studio 2010 nel progetto di database di SQL Server Data Tools.|  
|[Procedura: Specificare script pre-distribuzione o post-distribuzione](../ssdt/how-to-specify-predeployment-or-postdeployment-scripts.md)|Viene illustrato come utilizzare gli script da eseguire prima o dopo la distribuzione del database.|  
  
## <a name="related-sections"></a>Sezioni correlate

[Gestire tabelle e relazioni e correggere errori](../ssdt/manage-tables-relationships-and-fix-errors.md)
