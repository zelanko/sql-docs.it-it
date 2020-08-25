---
title: Creare frammenti di codice riutilizzabili
description: Informazioni su come creare e usare frammenti di codice SQL di Azure Data Studio, che semplificano la creazione di database e oggetti di database.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 95b0385178a5e2bd25f8b64be5f910d4f885e34b
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746091"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-azure-data-studio"></a>Creare e usare frammenti di codice per creare rapidamente script Transact-SQL (T-SQL) in Azure Data Studio

In Azure Data Studio i frammenti di codice sono modelli che consentono di creare facilmente database e oggetti di database. 

In Azure Data Studio sono disponibili vari frammenti di codice T-SQL che consentono di generare rapidamente la sintassi corretta. 

È possibile creare anche frammenti di codice definiti dall'utente.

## <a name="using-built-in-t-sql-code-snippets"></a>Uso di frammenti di codice T-SQL predefiniti

1. Per accedere ai frammenti di codice disponibili, digitare *sql* nell'editor di query per aprire l'elenco:

   ![frammenti](media/code-snippets/sql-snippets.png)

1. Selezionare il frammento di codice che si vuole usare, da cui verrà generato lo script T-SQL. Selezionare, ad esempio, *sqlCreateTable*:

   ![Creazione di frammenti di codice di tabella](media/code-snippets/create-table.png)

1. Aggiornare i campi evidenziati con i valori specifici appropriati. Sostituire, ad esempio, *TableName* e *Schema* con i valori relativi al database in uso:

   ![sostituzione di un campo del modello](media/code-snippets/table-from-snippet.png)

   Se il campo che si vuole modificare non è più evidenziato (questo errore si verifica quando si sposta il cursore all'interno dell'editor), fare clic con il pulsante destro del mouse sulla parola che si vuole modificare e selezionare **Modifica tutte le occorrenze**:

   ![sostituzione di un campo del modello](media/code-snippets/change-all.png)

1. Aggiornare o aggiungere gli script T-SQL necessari per il frammento di codice selezionato. Aggiornare, ad esempio, *Column1* e *Column2* e aggiungere altre colonne.


 
## <a name="creating-sql-code-snippets"></a>Creazione di frammenti di codice T-SQL 

È possibile definire frammenti di codice personalizzati. Per aprire il file del frammento di codice SQL da modificare:

1. Aprire il *Riquadro comandi* (**MAIUSC + CTRL + P**), digitare *snip* e selezionare **Preferenze: Apri frammenti di codice utente**:

   ![sostituzione di un campo del modello](media/code-snippets/user-snippets.png)

1. Selezionare **SQL**:

   > [!NOTE]
   > Azure Data Studio eredita la funzionalità dei frammenti di codice da Visual Studio Code ed è per questo motivo che questo articolo analizza nello specifico l'uso di frammenti di codice SQL. Per informazioni più dettagliate, vedere [Creazione di frammenti di codice personalizzati](https://code.visualstudio.com/docs/editor/userdefinedsnippets) nella documentazione di Visual Studio Code. 

   ![sostituzione di un campo del modello](media/code-snippets/select-sql.png)

1. Incollare il codice seguente in *sql.json*:

   ```sql
   {
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   }
   ```

1. Salvare il file sql.json.
1. Aprire una nuova finestra dell'editor di query facendo clic su **CTRL + N**.
2. Digitare **sql** per visualizzare i due frammenti di codice utente appena aggiunti: *sqlCreateTable2* e *sqlSelectTop5*.

Selezionare uno dei nuovi frammenti di codice e provarlo.


## <a name="additional-resources"></a>Risorse aggiuntive

Per informazioni sull'editor SQL, vedere [Esercitazione sull'editor di codice](tutorial-sql-editor.md).
