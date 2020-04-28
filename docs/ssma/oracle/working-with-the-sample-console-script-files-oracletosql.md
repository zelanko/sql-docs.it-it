---
title: Uso dei file script della console di esempio (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sample Console Script Files, ServersConnectionFileSample.xml
- Sample Console Script Files, SqlStatementConversionSample.xml
- Sample Console Script Files,VariableValueFileSample.xml
ms.assetid: c6202dcc-b994-457b-9b2f-0cd89e79792d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fbe3e8c07af283f657926776e906dca4a95f7a7e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68259597"
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>Uso dei file script di esempio della console (OracleToSQL)
Sono stati forniti alcuni file di esempio insieme al prodotto per il riferimento utente e l'utilizzo. In questa sezione viene descritto come personalizzare facilmente questi script in base alle esigenze dell'utente finale.  
  
## <a name="sample-console-script-files"></a>File script della console di esempio  
Per informazioni di riferimento sull'utente sono stati forniti i file script della console di esempio seguenti relativi a diversi scenari:  
  
-   ServersConnectionFileSample. XML  
  
-   VariableValueFileSample. XML  
  
-   AssessmentReportGenerationSample. XML  
  
-   SqlStatementConversionSample. XML  
  
-   ConversionAndDataMigrationSample. XML  
  
-   **ServersConnectionFileSample. XML:**  
  
    -   In questo esempio vengono fornite le diverse modalità di connessione disponibili per il database di origine e di destinazione e l'utente può selezionare qualsiasi modalità in base al requisito. Questo esempio contiene le definizioni del server.  
  
    -   L'utente può connettersi al database necessario semplicemente modificando i valori delle definizioni del server di origine e di destinazione richieste. Nell'esempio, tutti i valori sono stati forniti come valori variabili disponibili in **VariableValueFileSample. XML**.  Tutti gli altri parametri di connessione possono essere rimossi dal file di connessione del server funzionante dell'utente.  
  
    -   Per ulteriori informazioni sulla connessione al server di origine e di destinazione, vedere [creazione dei file di connessione al server &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) .  
  
-   **VariableValueFileSample. XML:** Tutte le variabili usate nei file script della console di esempio e `ServersConnectionFileSample.xml` sono state confrontate in questo file. Per eseguire gli script della console di esempio, l'utente deve semplicemente sostituire i valori delle variabili di esempio con quelli definiti dall'utente e passare il file come argomento della riga di comando aggiuntivo insieme al file di script.  
  
    Per altre informazioni sul file di valori di variabile, vedere [creazione di file di valori di variabile &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
-   **AssessmentReportGenerationSample. XML:** Questo esempio consente all'utente di generare un report di valutazione XML che può essere utilizzato dall'utente per l'analisi prima di iniziare la conversione e la migrazione dei dati.  
  
    Nel `generate-assessment-report` comando l'utente deve obbligatoriamente modificare il valore della variabile (vedere **VariableValueFileSample. XML**) nell' `object-name` attributo per il nome del database usato dall'utente. A seconda del tipo di oggetto specificato, sarà necessario `object-type` modificare anche il valore.  
  
    Se l'utente deve valutare più oggetti/database, può specificare più `metabase-object` nodi, come illustrato nell'esempio `generate-assessment-report` di comando 4 del file script della console di esempio.  
  
    Per ulteriori informazioni sulla generazione di report, vedere [generazione di report &#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
    > [!NOTE]  
    > -   Verificare che l'argomento della riga di comando file valore variabile venga passato all'applicazione console e che VariableValueFileSample. XML venga aggiornato con i valori specificati dall'utente.  
    > -   Verificare che l'argomento della riga di comando del file di connessione del server venga passato all'applicazione console e che ServersConnectionFileSample. XML venga aggiornato con i valori dei parametri del server corretti.  
  
-   **SqlStatementConversionSample. XML:**  
    Questo esempio consente all'utente di generare lo script `t-sql` corrispondente per il comando del `sql` database di origine fornito come input.  
  
    Nel `convert-sql-statement` comando l'utente deve obbligatoriamente modificare il valore della variabile (fare riferimento a **VariableValueFileSample. XML**) nell' `context` attributo al nome del database in uso da parte dell'utente. L'utente dovrà anche modificare il `sql` valore dell'attributo con il comando del database `sql` di origine che richiede la conversione.  
  
    L'utente può inoltre fornire i file SQL da convertire. Questo è stato illustrato nell'esempio `convert-sql-statement` 4 del comando del file script della console di esempio.  
  
    > [!NOTE]  
    > Verificare che l'argomento della riga di comando file valore variabile venga passato all'applicazione console e che VariableValueFileSample. XML venga aggiornato con i valori specificati dall'utente.  
  
-   **ConversionAndDataMigrationSample. XML:**  
     Questo esempio consente all'utente di eseguire una migrazione end-to-end dalla conversione alla migrazione dei dati. L'elenco dei valori di attributo obbligatori che dovranno essere modificati è elencato di seguito:  
  
    **Nome comando**  
  
    `map-schema`  
  
    Mapping dello schema del database di origine allo schema di destinazione.  
  
    **Attributo**  
  
    -   `source-schema:`Specifica il database di origine che richiede la conversione.  
  
    -   `sql-server-schema`: Specifica il database di destinazione di cui eseguire la migrazione  
  
    **Nome comando**  
  
    `convert-schema`  
  
    -   Esegue la conversione dello schema dall'origine allo schema di destinazione.  
  
    -   Se l'utente deve valutare più oggetti/database, può specificare più `metabase-object` nodi, come illustrato nell'esempio `convert-schema` di comando 4 del file script della console di esempio.  
  
    **Attributo**  
  
    `object-name`: Specificare il nome del database o dell'oggetto di origine che richiede la conversione. Verificare che il corrispondente `object-type` venga modificato in base al tipo di oggetto specificato nel parametro`object-name`  
  
    **Nome comando**  
  
    `synchronize-target`  
  
    -   Sincronizza gli oggetti di destinazione con il database di destinazione.  
  
    -   Se l'utente deve valutare più oggetti/database, può specificare più `metabase-object` nodi, come illustrato nell' `synchronize-target` esempio 3 del file di script della console di esempio.  
  
    **Attributo**  
  
    `object-name:`Specificare il nome del database/oggetto di SQL Server che deve essere creato. Verificare che il corrispondente `object-type` venga modificato in base al tipo di oggetto specificato nel parametro`object-name`  
  
    **Nome comando**  
  
    `migrate-data`  
  
    -   Esegue la migrazione dei dati di origine alla destinazione.  
  
    -   Se l'utente deve valutare più oggetti/database, può specificare più `metabase-object` nodi, come illustrato nell' `migrate-data` esempio 2 del file di script della console di esempio.  
  
    **Attributo**  
  
    `object-name:`Specifica il nome del database o delle tabelle di origine che richiede la migrazione. Verificare che il corrispondente `object-type` venga modificato in base al tipo di oggetto specificato nel parametro`object-name`  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di file di valori di variabile &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[Creazione dei file di connessione del server &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[Generazione di report &#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
