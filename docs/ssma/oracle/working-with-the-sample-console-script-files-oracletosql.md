---
title: Lavorare con i file di Script di esempio Console (OracleToSQL) | Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: 152d8ba2964c8485a1f158b71717067fdea948a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743923"
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>Uso dei file script di esempio della console (OracleToSQL)
Alcuni file di esempio sono stati forniti insieme al prodotto per il riferimento all'utente e l'utilizzo. In questa sezione descrive il modo con facilità personalizzare questi script per soddisfare le esigenze degli utenti finali.  
  
## <a name="sample-console-script-files"></a>File di Script di esempio Console  
I seguenti file script di esempio console relativi a diversi scenari sono stati forniti i riferimenti all'utente:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   In questo esempio offre diverse modalità di connessione disponibili per il database di origine e destinazione e l'utente può selezionare qualsiasi modalità in base al requisito. In questo esempio contiene le definizioni di Server.  
  
    -   L'utente può connettersi al database obbligatorio modificando semplicemente i valori per l'origine necessari e le definizioni dei server di destinazione. Nell'esempio fornito tutti i valori sono stati forniti valori come variabili che sono disponibili nel **VariableValueFileSample.xml**.  Tutti gli altri parametri di connessione possono essere rimosso dal file di connessione server di lavoro dell'utente.  
  
    -   Per altre informazioni sulla connessione al server di origine e di destinazione, vedere [creazione di file di connessione del Server &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) .  
  
-   **VariableValueFileSample.xml:** Tutte le variabili che sono state utilizzate nella console di esempio i file di script e `ServersConnectionFileSample.xml` sono stati confrontati in questo file. Per eseguire gli script di esempio console che l'utente deve semplicemente sostituire la variabile di esempio i valori con l'utente definito quelle e passare questo file come un argomento della riga di comando aggiuntivi insieme al file di script.  
  
    Per altre informazioni sul File con valori variabili, vedere [creazione di file di valore variabile &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** In questo esempio consente all'utente generare un report di valutazione di xml che può essere utilizzato dall'utente per l'analisi prima che inizi a convertire e la migrazione dei dati.  
  
    Nel `generate-assessment-report` l'utente deve modificare obbligatoriamente includere il valore della variabile di comando (fare riferimento **VariableValueFileSample.xml**) nella `object-name` attributo al nome di database da in uso dall'utente. A seconda del tipo dell'oggetto specificato, il `object-type` valore dovrà inoltre essere modificato.  
  
    Se l'utente dispone valutare più oggetti / database è possibile specificare più `metabase-object` nodi come illustrato nella `generate-assessment-report` 4 di esempio del comando del file di script di esempio console.  
  
    Per altre informazioni sulla generazione di report, vedere [generazione di report &#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
    > [!NOTE]  
    > -   Assicurarsi che l'argomento della riga di comando file valore della variabile viene passato all'applicazione console e VariableValueFileSample.xml viene aggiornato con l'utente specificato i valori.  
    > -   Assicurarsi che l'argomento della riga di comando file connessione server viene passato all'applicazione console e il ServersConnectionFileSample.xml viene aggiornata con i valori dei parametri server corretto.  
  
-   **SqlStatementConversionSample.xml:**  
    In questo esempio consente all'utente genera il corrispondente `t-sql` script per database di origine `sql` comando fornito come input.  
  
    Nel `convert-sql-statement` l'utente deve modificare obbligatoriamente includere il valore della variabile di comando (fare riferimento **VariableValueFileSample.xml**) nel `context` attributo al nome del database che è in corso in uso dall'utente. L'utente sarà inoltre necessario modificare il `sql` valore dell'attributo per il database di origine `sql` comando che può richiedere da convertire.  
  
    L'utente può anche fornire i file sql da convertire. Questa operazione è stata illustrata nel `convert-sql-statement` 4 di esempio del comando del file di script di esempio console.  
  
    > [!NOTE]  
    > Assicurarsi che l'argomento della riga di comando file valore della variabile viene passato all'applicazione console e VariableValueFileSample.xml viene aggiornato con l'utente specificato i valori.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     In questo esempio consente all'utente di eseguire una migrazione end-to-end dalla conversione per la migrazione dei dati. L'elenco di valori di attributo obbligatorio che dovranno cambiare è elencato di seguito:  
  
    **Nome del comando**  
  
    `map-schema`  
  
    Mapping dello schema del database di origine allo schema di destinazione.  
  
    **Attribute**  
  
    -   `source-schema:` Specifica il database di origine che richiede da convertire.  
  
    -   `sql-server-schema`: Specifica il database di destinazione che deve essere eseguita la migrazione a  
  
    **Nome del comando**  
  
    `convert-schema`  
  
    -   Esegue la conversione dello schema di origine allo schema di destinazione.  
  
    -   Se l'utente dispone valutare più oggetti / database è possibile specificare più `metabase-object` nodi come illustrato nella `convert-schema` 4 di esempio del comando del file di script di esempio console.  
  
    **Attribute**  
  
    `object-name`: Specificare il database di origine / nome che richiede la conversione dell'oggetto. Assicurarsi che la corrispondente `object-type` viene modificato in base al tipo di oggetto specificato di `object-name`  
  
    **Nome del comando**  
  
    `synchronize-target`  
  
    -   Sincronizza gli oggetti di destinazione con il database di destinazione.  
  
    -   Se l'utente dispone valutare più oggetti / database è possibile specificare più `metabase-object` nodi come illustrato nella `synchronize-target` 3 di esempio del comando del file di script di esempio console.  
  
    **Attribute**  
  
    `object-name:` Specificare il database di sql server / nome che richiede la creazione dell'oggetto. Assicurarsi che la corrispondente `object-type` viene modificato in base al tipo di oggetto specificato di `object-name`  
  
    **Nome del comando**  
  
    `migrate-data`  
  
    -   Esegue la migrazione dei dati di origine alla destinazione.  
  
    -   Se l'utente dispone valutare più oggetti / database è possibile specificare più `metabase-object` nodi come illustrato nella `migrate-data` 2 di esempio del comando del file di script di esempio console.  
  
    **Attribute**  
  
    `object-name:` Specifica il database di origine / nome che è necessario eseguire la migrazione di tabelle. Assicurarsi che la corrispondente `object-type` viene modificato in base al tipo di oggetto specificato di `object-name`  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di file di valore della variabile &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[Creazione di file di connessione del Server &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[Generating Reports &#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
