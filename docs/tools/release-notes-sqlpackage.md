---
title: Note sulla versione di DacFx e SqlPackage | Microsoft Docs
description: Note sulla versione di sqlpackage Microsoft.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538777"
---
# <a name="release-notes-for-sqlpackageexe"></a>Note sulla versione per SqlPackage.exe

**[Scaricare la versione più recente](sqlpackage-download.md)**

Questo articolo elenca le funzionalità e correzioni recapitate da versioni diverse di SqlPackage.exe.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>sqlpackage 18.1

Data di rilascio: &nbsp; 1 febbraio 2019  
Build: &nbsp; 15.0.4316.1  
Versione di anteprima.

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Aggiunta del supporto per le regole di confronto UTF8. | &nbsp; |
| Abilitare gli indici columnstore non cluster su una vista indicizzata. | &nbsp; |
| Spostare in .NET Core 2.2. | &nbsp; |
| Usare l'archiviazione di memoria supportata per confronto schema in .NET Core. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Le prestazioni correggere utilizzare lo strumento di stima di cardinalità legacy per le query engineering inverse. | &nbsp; |
| Risolto un problema di prestazioni del confronto schema significativo durante la generazione di uno script. | &nbsp; |
| Risolto la logica di rilevamento di deviazione di schema per ignorare alcune sessioni eventi estesi (xevent). | &nbsp; |
| Ordinamento di tabelle grafi importazione fisso. | &nbsp; |
| Correzione di tabelle esterne con autorizzazioni per oggetti di esportazione. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Questa versione include le compilazioni cross-platform preview di sqlpackage destinate a .NET Core 2.2. Sqlpackage eseguibili in macOS e Linux.

| Problema noto | Dettagli |
| :---------- | :------ |
| Non sono supportati i collaboratori di compilazione e distribuzione. | &nbsp; |
| File con estensione dacpac e bacpac meno recenti che usano la serializzazione dei dati json non sono supportati. | &nbsp; |
| Riferimento .dacpacs (ad esempio master.dacpac) non possono essere risolti a causa di problemi con i sistemi di file tra maiuscole e minuscole. | Soluzione alternativa consiste nel convertire in maiuscolo il nome del file di riferimento (ad esempio MASTER. FILE BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>sqlpackage 18.0

Data di rilascio: &nbsp; 24 ottobre 2018  
Build: &nbsp; 15.0.4200.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Aggiunta del supporto per il livello di compatibilità database 150. | &nbsp; |
| Aggiunta del supporto per le istanze gestite. | &nbsp; |
| Aggiunta MaxParallelism del parametro della riga di comando per specificare il grado di parallelismo per le operazioni di database. | &nbsp; |
| Aggiunta AccessToken del parametro della riga di comando per specificare un token di autenticazione quando ci si connette a SQL Server. | &nbsp; |
| Aggiunta del supporto per i tipi di dati BLOB/CLOB di flusso per le importazioni. | &nbsp; |
| Aggiunta del supporto per UDF scalari opzione 'INLINE'. | &nbsp; |
| Aggiunta del supporto per la sintassi 'MERGE' nella tabella di grafico. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Pseudo-colonna non risolto fissa per tabelle grafi. | &nbsp; |
| Correzione di creazione di un database con file con ottimizzazione per la memoria vengono usati gruppi di tabelle ottimizzate per la memoria. | &nbsp; |
| Risolto tra cui le proprietà estese per le tabelle esterne. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>sqlpackage 17.8

Data di rilascio: &nbsp; 22 giugno 2018  
Build: &nbsp; 14.0.4079.2

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Messaggi di errore per gli errori di connessione, tra cui il messaggio di eccezione SqlClient migliorati. | &nbsp; |
| Supporta la compressione dell'indice negli indici partizione singola per importazione/esportazione. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Risolto un problema reverse engineering per set di colonne XML con SQL 2017 e versioni successive. | &nbsp; |
| Risolto un problema in cui il livello di compatibilità 140 di script è stato ignorato per il Database SQL di Azure. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>sqlpackage 17.4.1

Data di rilascio: &nbsp; 25 gennaio 2018  
Build: &nbsp; 14.0.3917.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Aggiunta ThreadMaxStackSize del parametro della riga di comando per analizzare Transact-SQL con un numero elevato di istruzioni annidate. | &nbsp; |
| Supporto delle regole di confronto del catalogo di database. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Quando si importa un bacpac del Database SQL di Azure in un'istanza on-premise, correzione di errori a causa dell'errore _chiavi master di Database senza password non sono supportate in questa versione di SQL Server_. | &nbsp; |
| Correzione di un errore di colonna pseudo non risolti per tabelle grafi. | &nbsp; |
| Risolto tramite il SchemaCompareDataModel con autenticazione di SQL Server per confrontare gli schemi. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>sqlpackage 17.4.0

Data di rilascio: &nbsp; 12 dicembre 2017  
Build: &nbsp; 14.0.3881.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Aggiunta del supporto per _criteri di conservazione temporale_ su SQL 2017 + e Database SQL di Azure. | &nbsp; |
| Aggiunto /DiagnosticsFile:"C:\Temp\sqlpackage.log" parametro della riga di comando per specificare un percorso di file per salvare le informazioni di diagnostica. | &nbsp; |
| Parametro della riga di comando /Diagnostics aggiunto per registrare le informazioni di diagnostica nella console. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Non vengono bloccati in presenza di un livello di compatibilità del database che non è stato riconosciuto. | Al contrario, verrà considerata come la piattaforma più recente di Database SQL di Azure o in locale. |
| &nbsp; | &nbsp; |
