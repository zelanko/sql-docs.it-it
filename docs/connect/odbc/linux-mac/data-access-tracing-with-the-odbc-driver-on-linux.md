---
title: Traccia di accesso ai dati con il driver ODBC in Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6abf282656681d3f798215282adb784b29c3846
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921987"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Traccia di accesso ai dati con il driver ODBC in Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Gestione driver unixODBC in macOS e Linux supporta la traccia delle chiamate all'API ODBC in ingresso e in uscita di ODBC Driver per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Per tracciare il comportamento ODBC dell'applicazione, modificare la sezione `[ODBC]` del file `odbcinst.ini` per impostare i valori `Trace=Yes` e `TraceFile` sul percorso del file che deve contenere l'output di traccia, ad esempio:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

È anche possibile usare `/dev/stdout` o un qualsiasi altro nome di dispositivo per inviare l'output di traccia invece di usare un file persistente. Con le impostazioni precedenti, ogni volta che un'applicazione carica Gestione driver unixODBC, vengono registrate tutte le chiamate all'API ODBC eseguite nel file di output.

Dopo aver completato la traccia dell'applicazione, rimuovere `Trace=Yes` dal file `odbcinst.ini` per evitare la riduzione delle prestazioni e controllare che tutti i file di traccia non necessari siano rimossi.

La traccia si applica a tutte le applicazioni che usano il driver in `odbcinst.ini`. Per non tracciare tutte le applicazioni, ad esempio per evitare di rivelare informazioni riservate dei singoli utenti, è possibile tracciare una singola istanza dell'applicazione specificando il percorso di un file `odbcinst.ini` privato tramite la variabile di ambiente `ODBCSYSINI`. Ad esempio:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

In questo caso è possibile aggiungere `Trace=Yes` alla sezione `[ODBC Driver 13 for SQL Server]` di `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Individuazione del file odbc.ini usato dal driver

I driver ODBC in Linux e macOS non conoscono il file `odbc.ini` in uso o il percorso del file `odbc.ini`. Informazioni sul file `odbc.ini` in uso sono tuttavia disponibili negli strumenti unixODBC `odbc_config` e `odbcinst` nella documentazione di Gestione driver unixODBC.

Ad esempio, il comando seguente stampa tra le altre informazioni il percorso dei file `odbc.ini` di sistema e dell'utente che contengono rispettivamente il DSN di sistema e dell'utente:

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

La [documentazione di unixODBC](http://www.unixodbc.org/doc/UserManual/) spiega le differenze tra i DSN utente e i DSN di sistema. In sintesi:

- DSN utente: sono DSN disponibili solo per un utente specifico. Gli utenti possono usarli per la connessione e possono aggiungere, modificare e rimuovere i propri DSN utente. I DSN utente sono archiviati in un file nella home directory dell'utente o in una sua sottodirectory.

- DSN di sistema: sono DSN disponibili per ogni utente del sistema per la connessione, ma possono essere aggiunti, modificati e rimossi solo da un amministratore di sistema. Se un utente dispone di un DSN utente con lo stesso nome di un DSN di sistema, il DSN utente verrà usato per le connessioni da tale utente.

## <a name="see-also"></a>Vedere anche

- [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)
