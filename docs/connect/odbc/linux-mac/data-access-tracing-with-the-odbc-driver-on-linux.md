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
manager: jroth
ms.openlocfilehash: cd71429e5a407e595cc3f65e73e984bfc12280b1
ms.sourcegitcommit: 5d27fb187006e676d652884f0c1f5133a1bd62b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67152219"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Traccia di accesso ai dati con il driver ODBC in Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

La gestione Driver unixODBC in macOS e Linux supporta la traccia di chiamate all'API ODBC in ingresso e uscita del Driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Per tracciare il comportamento dell'applicazione ODBC, modificare il `odbcinst.ini` del file `[ODBC]` sezione per impostare i valori `Trace=Yes` e `TraceFile` al percorso del file che conterrà la traccia di output; ad esempio:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(È anche possibile usare `/dev/stdout` o qualsiasi altro nome di dispositivo per l'invio di output sono invece che in un file permanente di analisi.) Con le impostazioni sopra riportate, ogni volta che un'applicazione carica la gestione Driver unixODBC registrerà tutte le chiamate di API ODBC che eseguita nel file di output.

Dopo aver completato la traccia dell'applicazione, rimuovere `Trace=Yes` dal `odbcinst.ini` file per evitare la riduzione delle prestazioni di traccia e assicurarsi di rimuovere eventuali file di traccia non necessari.

La traccia si applica a tutte le applicazioni che usano il driver in `odbcinst.ini`. Per non tracciare tutte le applicazioni, ad esempio per evitare di rivelare informazioni riservate dei singoli utenti, è possibile tracciare una singola istanza dell'applicazione specificando il percorso di un file `odbcinst.ini` privato tramite la variabile di ambiente `ODBCSYSINI`. Esempio:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

In questo caso, è possibile aggiungere `Trace=Yes` per il `[ODBC Driver 13 for SQL Server]` sezione `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Individuazione del file odbc.ini usato dal driver

I driver ODBC in Linux e macOS non conosce quale `odbc.ini` è in uso o il percorso di `odbc.ini` file. Tuttavia, informazioni su quali `odbc.ini` file è in uso è disponibile in strumenti unixODBC `odbc_config` e `odbcinst`e la documentazione di gestione Driver unixODBC.

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

Il [documentazione unixODBC](http://www.unixodbc.org/doc/UserManual/) vengono illustrate le differenze tra l'utente e DSN di sistema. In breve:

- I DSN utente---si tratta di DSN di cui sono disponibili solo per un utente specifico. Gli utenti possono connettersi tramite, aggiungere, modificare e rimuovere i propri DSN utente. DSN utente vengono archiviati in un file nella directory home dell'utente o una sottodirectory della stessa.

- DSN di sistema---questi DSN disponibili per ogni utente del sistema per la connessione con essi, ma può solo essere aggiunto, modificato e rimosso da un amministratore di sistema. Se un utente dispone di un DSN dell'utente con lo stesso nome di DSN di sistema, il DSN utente verrà utilizzato al momento le connessioni da tale utente.

## <a name="see-also"></a>Vedere anche

- [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)
