---
title: Limitazioni e problemi noti per SSIS in Linux
description: Questo articolo descrive le limitazioni e problemi noti per SQL Server Integration Services (SSIS) in computer Linux
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: jroth
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: bc4ec7f99a8cbcf5b6bd48924f3eed1e8f10f658
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833136"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitazioni e problemi noti per SSIS in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive le limitazioni e problemi noti per SQL Server Integration Services (SSIS) in Linux.

## <a name="general-limitations-and-known-issues"></a>Problemi noti e limitazioni generali

Le funzionalità seguenti non sono supportate in questa versione di SSIS in Linux:
  - Database del catalogo SSIS
  - Esecuzione del pacchetto pianificato da SQL Agent
  - Autenticazione di Windows
  - Componenti di terze parti
  - Change Data Capture (CDC)
  - SSIS Scale Out
  - Azure Feature Pack per SSIS
  - Supporto di Hadoop e HDFS
  - Microsoft Connector for SAP BW

Per altre limitazioni e problemi noti di SSIS in Linux, vedere la [note sulla versione](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a> Componenti supportati e non supportati

I seguenti componenti di Integration Services predefiniti sono supportati in Linux. Alcune di esse presentano limitazioni sulla piattaforma Linux. Componenti predefiniti che non sono elencati qui non sono supportati in Linux.

## <a name="supported-control-flow-tasks"></a>Attività flusso di controllo è supportato
- Inserimento bulk - attività
- Attività Flusso di dati
- Attività Profiling dati
- Attività Esegui SQL
- Attività Esegui istruzione T-SQL
- Attività Espressione
- Attività FTP
- Attività Servizio Web
- Attività XML

## <a name="control-flow-tasks-supported-with-limitations"></a>Attività flusso di controllo è supportata con limitazioni

| Attività | Limitazioni |
|------------|---|
| Execute Process Task | Supporta solo la modalità in-process. |
| Attività File system | Il *directory di spostamento* e *impostare gli attributi di file* azioni non sono supportate. |
| attività Script | Supporta solo l'API di .NET Framework standard. |
| Invia messaggi - attività | Supporta solo la modalità utente anonimo. |
| Attività Trasferisci Database | I percorsi UNC non sono supportati. |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>Attività piano di manutenzione supportati e non supportati

In un piano di manutenzione di SQL Server, è possibile usare in genere un'ampia gamma di attività SSIS.

La seguente attività di manutenzione non sono supportate in Linux:
- Notifica operatore
- Esegui processo di SQL Server Agent

La seguente attività di manutenzione sono supportate in Linux:
- Controlla integrità Database
- Compatta Database
- Riorganizza indice
- Ricompila indice
- Aggiorna statistiche
- Pulizia contenuto cronologia
- Eseguire il backup di Database
- Istruzione T-SQL

## <a name="supported-control-flow-containers"></a>Contenitori del flusso di controllo è supportato
- Sequenza - contenitore
- Contenitore Ciclo For
- Contenitore Ciclo Foreach

## <a name="supported-data-flow-sources-and-destinations"></a>Origini flusso di dati supportati e le destinazioni
- Destinazione e origine File non elaborato
- Origine XML

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Origini flusso di dati e destinazioni è supportate con limitazioni

| Componente | Limitazioni |
|------------|---|
| Destinazione e origine ADO.NET | Supportano solo il provider di dati SQLClient. |
| Destinazione e origine File flat | Supportano solo i percorsi di file basato su Windows, a cui viene applicata la regola di mapping di percorso predefinito. Ad esempio `D:\home\ssis\travel.csv` diventa `/home/ssis/travel.csv`. |
| Origine OData | Supporta solo l'autenticazione di base. |
| Origine e destinazione ODBC | Supporta i driver di Unicode ODBC a 64 bit in Linux. Dipende dalla Gestione driver UnixODBC in Linux. |
| Origine OLE DB e destinazione | Supportano solo SQL Server Native Client 11.0, Provider Microsoft OLE DB per SQL Server. |
| | |

## <a name="supported-data-flow-transformations"></a>Trasformazioni del flusso di dati è supportata
- Aggregate
- Audit
- Server di distribuzione di dati bilanciati
- Mappa caratteri
- Suddivisione condizionale
- Copia colonna
- Conversione dati
- Colonna derivata
- Esportazione colonna
- Raggruppamento fuzzy
- Ricerca fuzzy
- Importa colonna
- Ricerca
- Merge
- Merge Join
- Multicast
- Pivot
- Conteggio righe
- Dimensione a modifica lenta
- Ordina
- Ricerca termini
- Union All
- UnPivot

## <a name="data-flow-transformations-supported-with-limitations"></a>Trasformazioni del flusso di dati supportate con limitazioni

| Componente | Limitazioni |
|------------|---|
| Comando OLE DB - trasformazione | Stesse limitazioni dell'origine OLE DB e la destinazione. |
| componente script | Supporta solo l'API di .NET Framework standard. |
| | |

## <a name="supported-and-unsupported-log-providers"></a>Provider di log supportati e non supportati
Tutti i provider di log SSIS incorporati sono supportati in Linux tranne il provider del registro eventi di Windows.

Il provider di log di SQL Server supporta solo l'autenticazione di SQL. non supporta l'autenticazione di Windows.

I provider di log SSIS per file di testo, per i file XML e per SQL Server Profiler scrivono il proprio output a un file specificato. Le considerazioni seguenti si applicano al percorso del file:
-   Se non si specifica un percorso, il provider di log scrive nella directory corrente dell'host. Se l'utente corrente non dispone delle autorizzazioni di scrittura nella directory corrente dell'host, il provider di log genera un errore.
-   È possibile usare una variabile di ambiente in un percorso di file. Se si specifica una variabile di ambiente, viene visualizzato il testo letterale specificato nel percorso del file. Ad esempio, se si specifica `%TMP%/log.txt`, il provider di log consente di accodare il testo letterale `/%TMP%/log.txt` nella directory host corrente.

## <a name="related-content-about-ssis-on-linux"></a>Contenuto correlato su SSIS in Linux
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md)
-   [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Esecuzione in Linux con cron pacchetti pianificazione SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
