---
title: Problemi noti per il driver ODBC in Linux e macOS
description: Informazioni sui problemi noti relativi a Microsoft ODBC Driver for SQL Server in Linux e macOS e sui passaggi per la risoluzione dei problemi di connettività.
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1057252f896b62a5659b53aa53eb2f5c6d9b17ea
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288067"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Problemi noti per il driver ODBC in Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento contiene un elenco di problemi noti relativi a Microsoft ODBC Driver for SQL Server 13, 13.1 e 17 in Linux e macOS. Contiene anche i passaggi per la risoluzione dei problemi di connettività.

## <a name="known-issues"></a>Problemi noti

Ulteriori problemi verranno pubblicati nel [blog sui driver di SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers).  

- A causa delle limitazioni della libreria di sistema, Alpine Linux supporta meno codifiche di caratteri e impostazioni locali. Ad esempio, en_US.UTF-8 non è disponibile. Per altre informazioni, vedere [musl libc - functional differences from glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html) (musl libc - differenze funzionali da glibc).

- Windows, Linux e macOS convertono i caratteri provenienti dall'Area uso privato (PUA) o i caratteri definiti dall'utente finale (EUDC) in modo diverso. Per le conversioni eseguite sul server all'interno di [!INCLUDE[tsql](../../../includes/tsql-md.md)] viene usata la libreria di conversione Windows. Le conversioni eseguite nel driver usano le librerie di conversione Windows, Linux o macOS. Le conversioni eseguite con le due librerie possono produrre risultati diversi. Per altre informazioni, vedere [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caratteri definiti dall'utente finale e caratteri di area uso privato).

- Se la codifica del client è UTF-8, Gestione driver non esegue sempre correttamente la conversione da UTF-8 a UTF-16. Attualmente se uno o più caratteri della stringa non sono caratteri UTF-8 validi, i dati vengono danneggiati. I caratteri ASCII vengono mappati correttamente. Gestione driver tenta questa conversione quando si chiamano le versioni SQLCHAR dell'API ODBC (ad esempio, SQLDriverConnectA). Gestione driver non tenterà questa conversione quando si chiamano le versioni SQLWCHAR dell'API ODBC (ad esempio, SQLDriverConnectW).  

- Il parametro *ColumnSize* di **SQLBindParameter** fa riferimento al numero di caratteri nel tipo SQL, mentre *BufferLength* è il numero di byte nel buffer dell'applicazione. Tuttavia, se il tipo di dati SQL è `varchar(n)` o `char(n)`, se l'applicazione associa il parametro come SQL_C_CHAR o SQL_C_VARCHAR e se la codifica dei caratteri del client è UTF-8, è possibile che si verifichi un errore "Troncamento a destra della stringa di dati" nel driver anche se il valore di *ColumnSize* è allineato con la dimensione del tipo di dati nel server. Questo errore si verifica perché le conversioni tra codifiche di caratteri possono cambiare la lunghezza dei dati. Ad esempio un carattere virgoletta singola destra (U+2019) è codificato in CP-1252 come 0x92 a byte singolo, mentre in UTF-8 è codificato come sequenza a tre byte 0xe2 0x80 0x99.

Ad esempio se la codifica è UTF-8 e si specifica 1 sia per *BufferLength* sia per *ColumnSize* in **SQLBindParameter** per un parametro out, quindi si prova a recuperare il carattere precedente archiviato in una colonna `char(1)` nel server (usando CP-1252), il driver tenta di convertirlo alla codifica UTF-8 a 3 byte, ma non può adattare il risultato in un buffer di 1 byte. Nella direzione opposta, *ColumnSize* viene confrontato con *BufferLength* in **SQLBindParameter** prima della conversione tra le diverse tabelle codici su client e server. Poiché il valore 1 di *ColumnSize* è minore di un valore *BufferLength* di 3 (ad esempio), il driver genera un errore. Per evitare questo errore, verificare che la lunghezza dei dati dopo la conversione si adatti correttamente al buffer o alla colonna specificati. Si noti che *ColumnSize* non può essere maggiore di 8000 per il tipo `varchar(n)`.

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a> Risoluzione dei problemi relativi alla connessione  

Se non si riesce a stabilire una connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite il driver ODBC, usare le informazioni seguenti per individuare il problema.  
  
Il problema di connessione più comune è legato alla presenza di due copie di Gestione driver UnixODBC installate. Cercare /usr for libodbc\*.so\*. Se è presente più di una versione del file, è possibile che esistano più installazioni di Gestione driver. L'applicazione potrebbe utilizzare la versione non corretta.
  
Abilitare il log della connessione modificando il file `/etc/odbcinst.ini` affinché contenga la sezione seguente con questi elementi:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Se viene generato un altro errore di connessione e il file di registro non è visualizzato, è possibile che nel computer in uso esistano due copie di Gestione driver. In caso contrario, l'output del log avrà un aspetto analogo a quanto segue:  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 17 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Se la codifica dei caratteri ASCII è diversa da UTF-8, ad esempio: 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
Sono installate più copie di Gestione driver e l'applicazione usa quella sbagliata oppure Gestione driver non è stato compilato correttamente.  
  
Per altre informazioni sulla risoluzione dei problemi di connessione, vedere:  

- [Passaggi per risolvere i problemi di connettività di SQL](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [Risoluzione dei problemi di connettività di SQL Server 2005 - Parte I](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [Risoluzione dei problemi di connettività in SQL Server 2008 con il buffer circolare della connettività](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [Strumento di risoluzione dei problemi di autenticazione di SQL Server](/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>Passaggi successivi

Per le istruzioni di installazione per il driver ODBC, vedere gli articoli seguenti:

- [Installazione di Microsoft ODBC Driver for SQL Server in Linux](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Installazione di Microsoft ODBC Driver for SQL Server in macOS](install-microsoft-odbc-driver-sql-server-macos.md)

Per altre informazioni, vedere le [linee guida per la programmazione](programming-guidelines.md) e le [note sulla versione](release-notes-odbc-sql-server-linux-mac.md).  
