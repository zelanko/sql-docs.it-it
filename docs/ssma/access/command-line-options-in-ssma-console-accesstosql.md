---
title: Opzioni della riga di comando nella Console SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: fc8065bcfda3066fae31be982e25f054c07bca3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650765"
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>Opzioni della riga di comando nella Console SSMA (AccessToSQL)
Microsoft offre un solido set di opzioni della riga di comando per eseguire e controllare le attività SSMA. Le sezioni che seguono forniscono ulteriori dettagli.  
  
## <a name="command-line-options-in-the-ssma-console"></a>Opzioni della riga di comando nella Console SSMA  
È qui descritti la console di opzioni del comando.  
  
Ai fini di questa sezione, il termine 'option' è detta anche 'switch'.  
  
Opzioni non sono tra maiuscole e minuscole e può iniziare con uno di ' **-** 'o' **/** ' caratteri.  
  
Se si specificano opzioni, è obbligatorio che si specificano i parametri di opzione corrispondente.  
  
I parametri di opzione devono essere separati dal carattere opzione da spazi vuoti.  
  
**Esempi di sintassi:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
Devono specificare i nomi di cartella o file contenenti spazi tra virgolette doppie.  
  
L'output di voci della riga di comando e i messaggi di errore viene archiviato in STDOUT o in un file specificato.  
  
### <a name="script-file-option--sscript"></a>Opzione di file di script: -s o script  
Un parametro obbligatorio, il percorso/nome del file script specifica lo script di sequenze di comandi deve essere eseguito da SSMA.  
  
**Esempi di sintassi:**  
  
`C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>Opzione del file di valore della variabile: la variabile o - v  
Il file di valore della variabile è costituito da variabili utilizzate nel file di script. L'opzione è facoltativa. Se le variabili non dichiarate nel file delle variabili e usate nel file di script, l'applicazione genera un errore e termina l'esecuzione della console.  
  
**Esempi di sintassi:**  
  
-   Variabili definite in più file di valore della variabile, ad esempio uno con un valore predefinito e l'altra con un valore specifico dell'istanza quando applicabile. L'ultimo file di variabili specificata negli argomenti della riga di comando consideri le preferenze, nel caso in cui è presente una duplicazione delle variabili:  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>Opzione file di connessione del server: - c/serverconnection  
Questo file contiene informazioni di connessione server per ogni server. Ogni definizione del server è identificato da un ID Server univoco. Gli ID Server viene fatto riferimento nel file di script per i comandi correlati alla connessione.  
  
Definizione di server può essere una parte del file di connessione di server e/o file di script. Id del server nel file di script ha la precedenza sul file di connessione del server, nel caso in cui è presente una duplicazione dell'id del server.  
  
**Esempi di sintassi:**  
  
-   Gli ID del server vengono usati nel file di script. Sono definiti in un file di connessione server separato. Questo file Usa le variabili definite nel file di valore della variabile:  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definizione del server è incorporato nel file di script:  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opzione di output XML: - x / xmloutput [xmloutputfile]  
Questo comando viene utilizzato per l'output i messaggi di output del comando in formato xml alla console o in un file xml.  
  
Sono disponibili due opzioni per xmloutput, vale a dire:  
  
-   Se il percorso file non viene fornito dopo il cambio di xmloutput, l'output viene reindirizzato al file.  
  
    **Esempio di sintassi:**  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Se non viene specificato alcun percorso di file dopo il cambio di xmloutput, quindi il xmlout viene visualizzato nella console di se stesso.  
  
    **Esempio di sintassi:**  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>Opzione di file di log: -l/log  
Tutte le operazioni di SSMA nell'applicazione Console vengono registrate in un file di log e l'opzione è facoltativa. Se un file di log e il relativo percorso vengono specificati nella riga di comando, viene generato il log nel percorso specificato. In caso contrario, viene generato nella posizione predefinita.  
  
**Esempio di sintassi:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>Opzione di ambiente cartella del progetto: projectenvironment / -e  
Questa opzione facoltativa indica la cartella Impostazioni ambiente di progetto SSMA corrente.  
  
**Esempio di sintassi:**  
  
`C:\>SSMAforAccessConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option--psecurepassword"></a>Secure password-opzione: -p/securepassword  
Questa opzione indica la password crittografata per le connessioni al server. Differisce da tutte le altre opzioni che non esegue qualsiasi script o della Guida in tutte le attività relative alla migrazione, ma consente di gestire la crittografia della password per le connessioni del server usato nel progetto di migrazione.  
  
È possibile immettere qualsiasi altra opzione o la password come parametro della riga di comando. In caso contrario, viene generato un errore. Per altre informazioni, vedere la [la gestione delle password](managing-passwords-accesstosql.md) sezione.  
  
Il seguente delle opzioni secondarie sono supportate per `-p/securepassword`:  
  
-   Per aggiungere una password o aggiornare una password esistente, all'archiviazione protetta per un ID del Server specificato o per tutti gli ID del Server definito nel file di connessione del server:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   Per rimuovere la password crittografata dalla risorsa di archiviazione protetta dell'ID del Server specificato o per tutti gli ID del Server:  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   Per visualizzare un elenco di ID Server per cui la password viene crittografata:  
  
    `-p/securepassword -l/list`  
  
-   Per esportare le password archiviate in un archivio protetto a un file crittografato. Questo file è crittografato con la frase di pass specificato dall'utente.  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   Crittografati-che è stato esportato in precedenza viene importato il file nell'archivio locale protetto utilizzando specificato dall'utente-passphrase. Una volta che il file viene decrittografato, questo viene archiviato in un nuovo file, che a sua volta, viene crittografato nel computer locale.  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    È possibile specificare più ID Server usando i separatori virgola.  
  
### <a name="help-option--help"></a>Help (opzione):-? /help  
Visualizza il riepilogo di sintassi delle opzioni della Console SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
Per una visualizzazione tabulare delle opzioni della riga di comando di Console SSMA, consultare [appendice - 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option--securepassword--help"></a>Opzione della Guida SecurePassword: - securepassword-? /Help  
Visualizza il riepilogo di sintassi delle opzioni della Console SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
Per una visualizzazione tabulare delle opzioni della riga di comando di Console SSMA, consultare [appendice - 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo dipende dai requisiti progetto:  
  
1.  Per specificare una password o l'esportazione / importazione per le password, vedere [la gestione delle password &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  Per la generazione di report, vedere [generazione di report &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  Per risolvere i problemi nella console, vedere [Troubleshooting &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
