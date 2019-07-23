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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008818"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Traccia di accesso ai dati con il driver ODBC in Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Gestione driver unixODBC in macOS e Linux supporta la traccia delle chiamate all'API ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]l'ingresso e l'uscita del driver ODBC.

Per tracciare il comportamento ODBC dell'applicazione, modificare `odbcinst.ini` la `[ODBC]` sezione del file per impostare i `Trace=Yes` valori `TraceFile` e sul percorso del file che deve contenere l'output di traccia, ad esempio:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(È anche possibile usare `/dev/stdout` o qualsiasi altro nome di dispositivo per inviare l'output di traccia invece di un file persistente). Con le impostazioni precedenti, ogni volta che un'applicazione carica Gestione driver unixODBC, registrerà tutte le chiamate API ODBC eseguite nel file di output.

Al termine della traccia dell'applicazione, rimuovere `Trace=Yes` `odbcinst.ini` dal file per evitare la riduzione delle prestazioni della traccia e verificare che i file di traccia non necessari vengano rimossi.

La traccia si applica a tutte le applicazioni che usano il driver in `odbcinst.ini`. Per non tracciare tutte le applicazioni, ad esempio per evitare di rivelare informazioni riservate dei singoli utenti, è possibile tracciare una singola istanza dell'applicazione specificando il percorso di un file `odbcinst.ini` privato tramite la variabile di ambiente `ODBCSYSINI`. Esempio:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

In questo caso, è possibile aggiungere `Trace=Yes` `[ODBC Driver 13 for SQL Server]` alla sezione di `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Individuazione del file odbc.ini usato dal driver

I driver ODBC Linux e MacOS non sanno quale `odbc.ini` sia in uso o il percorso `odbc.ini` del file. Tuttavia, le informazioni sul `odbc.ini` file in uso sono disponibili negli strumenti `odbc_config` unixODBC e `odbcinst`nella documentazione di gestione driver unixodbc.

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

La [documentazione di unixODBC](http://www.unixodbc.org/doc/UserManual/) illustra le differenze tra i DSN utente e di sistema. In breve:

- I DSN utente---sono DSN disponibili solo per un utente specifico. Gli utenti possono connettersi usando, aggiungono, modificano e rimuovono i propri DSN utente. I DSN utente vengono archiviati in un file nella home directory dell'utente o in una sottodirectory.

- I DSN di sistema---questi DSN sono disponibili per ogni utente del sistema per la connessione utilizzandoli, ma possono essere aggiunti, modificati e rimossi solo da un amministratore di sistema. Se un utente dispone di un DSN utente con lo stesso nome di un DSN di sistema, il DSN utente verrà usato al momento delle connessioni da tale utente.

## <a name="see-also"></a>Vedere anche

- [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)
