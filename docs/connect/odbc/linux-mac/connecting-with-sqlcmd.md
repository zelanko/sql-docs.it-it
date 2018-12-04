---
title: La connessione con sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21021402a10494306a3b667c5f7b83977dc7d205
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512545"
---
# <a name="connecting-with-sqlcmd"></a>Connessione con sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

L'utilità [sqlcmd](https://go.microsoft.com/fwlink/?LinkID=154481) è disponibile in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS.
  
I comandi seguenti mostrano come usare l'autenticazione di Windows (Kerberos) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] l'autenticazione, rispettivamente:
  
```  
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Opzioni disponibili

Nella versione corrente, sono disponibili le opzioni seguenti:  
  
- -? Visualizzazione `sqlcmd` utilizzo.  
  
- -a Richiede la dimensione di un pacchetto.  
  
- -b Termina il processo batch se viene rilevato un errore.  
  
- -c *batch_terminator* specificare il carattere di terminazione di batch.  
  
- -C Considera attendibile il certificato del server.  

- -d *database_name* problema un `USE ` *database_name* istruzione quando si avvia `sqlcmd`.  

- -D Indica che il valore passato all'opzione -S di `sqlcmd` deve essere interpretato come nome dell'origine dati (DSN). Per altre informazioni, vedere "Supporto di DSN in `sqlcmd` e `bcp`" alla fine di questo argomento.  
  
- -e Scrive gli script di input nel dispositivo di output standard (stdout).

- Usa una connessione trusted e l'autenticazione integrata. Per altre informazioni su come rendere attendibili le connessioni che usano l'autenticazione integrata da un client Linux o macOS, vedere [Using Integrated Authentication](../../../connect/odbc/linux-mac/using-integrated-authentication.md).

- -h *numero_di_righe* Specifica il numero di righe da stampare tra le intestazioni delle colonne.  
  
- -H Specifica il nome di una workstation.  
  
- -i *file_input*[,*file_input*[,…]] Identifica il file che contiene un batch di istruzioni o stored procedure SQL.  
  
- -I Set di `SET QUOTED_IDENTIFIER` opzione di connessione su ON.  
  
- -k Rimuove o sostituisce i caratteri di controllo.  
  
- **-K**_applicazione\_intent_  
Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. L'unico valore attualmente supportato è **ReadOnly**. Se l'opzione **-K** non è specificata, `sqlcmd` non supporta la connettività a una replica secondaria in un gruppo di disponibilità AlwaysOn. Per altre informazioni, vedere [Driver ODBC in Linux e macOS - disponibilità elevata e ripristino di emergenza](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-K** non è supportata in CTP per SUSE Linux. È tuttavia possibile specificare la parola chiave **ApplicationIntent=ReadOnly** in un file DSN passato a `sqlcmd`. Per altre informazioni, vedere "Supporto di DSN in `sqlcmd` e `bcp`" alla fine di questo argomento.  
  
- -l *timeout* Specifica il numero di secondi che devono trascorrere prima che si verifichi il timeout di un accesso a `sqlcmd` quando si tenta la connessione a un server.

- -m *livello_errore* Controlla i messaggi di errore inviati a stdout.  
  
- **-M**_a più subnet\_failover_  
Specificare sempre **-M** in caso di connessione al listener di un gruppo di disponibilità di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. **-M** consente un rilevamento più veloce dei failover e una connessione più rapida al server attualmente attivo. Se non si specifica **-M**, significa che l'opzione **-M** è disattivata. Per altre informazioni sulle [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], vedere [Driver ODBC in Linux e macOS - disponibilità elevata e ripristino di emergenza](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-M** non è supportata in CTP per SUSE Linux. È tuttavia possibile specificare la parola chiave **MultiSubnetFailover=Yes** in un file DSN passato a `sqlcmd`. Per altre informazioni, vedere "Supporto di DSN in `sqlcmd` e `bcp`" alla fine di questo argomento.  
  
- -N Crittografa la connessione.  
  
- -o *file_output*Identifica il file che riceve l'output di `sqlcmd`.  
  
- -p Stampa le statistiche delle prestazioni per ogni set di risultati.  
  
- -P Specifica una password utente.  
  
- -q *commandline_query* eseguire una query quando `sqlcmd` viene avviato, ma non viene chiuso al termine dell'esecuzione della query.  

- -Q *commandline_query* eseguire una query quando `sqlcmd` viene avviato. `sqlcmd` verrà chiuso al termine della query.  

- -r Reindirizza i messaggi di errore a stderr.

- -R Imposta il driver in modo che usi le impostazioni internazionali del client in caso di conversione dei dati relativi a valuta, data e ora in dati di tipo carattere. Attualmente viene usato solo il formato en_US (inglese Stati Uniti).
  
- -s *column_separator_char* specificare il carattere separatore di colonna.  

- -S [*protocol*:] *server*[**,**_port_]  
Specificare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per connettersi a, o se -D viene usata, un DSN. Il driver ODBC in Linux e macOS richiede - S. Si noti che **tcp** è l'unico protocollo valido.  
  
- -t *timeout_query* Specifica il numero di secondi prima del timeout di un comando o di un'istruzione SQL.  
  
- -u Specifica l'archiviazione di file_output in formato Unicode, indipendentemente dal formato di file_input.  
  
- -U *login_id* specificare un ID di accesso utente.  
  
- -V *livello_gravità_errore* Controlla il livello di gravità usato per impostare la variabile ERRORLEVEL.  
  
- -w *column_width* specificare la larghezza della schermata per l'output.  
  
- -W Rimuove gli spazi finali da una colonna.  
  
- -x Disabilita la sostituzione delle variabili.  
  
- -X Disabilita i comandi, lo script di avvio e le variabili di ambiente.  
  
- -y *variable_length_type_display_width* impostare il `sqlcmd` variabile di scripting `SQLCMDMAXFIXEDTYPEWIDTH`.
  
- -Y *fixed_length_type_display_width* impostare il `sqlcmd` variabile di scripting `SQLCMDMAXVARTYPEWIDTH`.


## <a name="available-commands"></a>Comandi disponibili

Nella versione corrente, sono disponibili i comandi seguenti:  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*conteggio*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>Opzioni non disponibili
Nella versione corrente non sono disponibili le opzioni seguenti:  

- -A Stabilisce la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite una connessione amministrativa dedicata (DAC, Dedicated Administrator Connection). Per informazioni su come effettuare una connessione amministrativa dedicata (DAC), vedere [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
- -f *tabella_codici* Specifica le tabelle codici di input e output.  
  
- -L Elenca i computer server configurati localmente e i nomi dei computer server che trasmettono in rete.  
  
- -v Crea una variabile di scripting di `sqlcmd` che può essere usata in uno script `sqlcmd`.  
  
È possibile usare il seguente metodo alternativo: inserire i parametri all'interno di un file, è quindi possibile aggiungere a un altro file. Ciò consentirà di usare un file di parametri per sostituire i valori. Creare ad esempio un file denominato `a.sql` (file dei parametri) con il contenuto seguente:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
Creare quindi un file denominato `b.sql` con i parametri per la sostituzione:  
  
    select $(ColumnName) from $(TableName)  

Nella riga di comando, combinare `a.sql` e `b.sql` in `c.sql` usando i comandi seguenti:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
Eseguire `sqlcmd` e usare `c.sql` come file di input:  
  
    slqcmd -S<...> -P<..> -U<..> -I c.sql  

- -z *password* Cambia password.  
  
- -Z *password* modificare la password e uscita.  

## <a name="unavailable-commands"></a>Comandi non disponibili

Nella versione corrente non sono disponibili i comandi seguenti:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>Supporto di DSN in sqlcmd e bcp

È possibile specificare un nome origine dati (DSN, Data Source Name) anziché un nome server nell'opzione **sqlcmd** o **bcp** `-S` (o nel comando **sqlcmd** :Connect) se si specifica -D. -D fa sì che **sqlcmd** oppure **bcp** per connettersi al server specificato nel DSN per l'opzione -S.  
  
DSN di sistema vengono archiviate nel `odbc.ini` file nella directory SysConfigDir ODBC (`/etc/odbc.ini` nelle installazioni standard). DSN utente vengono archiviati `.odbc.ini` nella home directory dell'utente (`~/.odbc.ini`).
  
In un DSN in Linux o macOS sono supportate le voci seguenti:

-   **ApplicationIntent=ReadOnly**  

-   **Database =**_database\_nome_  
  
-   **Driver = ODBC Driver 11 for SQL Server** o **Driver = ODBC Driver 13 for SQL Server**
  
-   **MultiSubnetFailover=Yes**  
  
-   **Server =**_server\_name\_oppure\_IP\_indirizzo_  
  
-   **Trusted_Connection=yes**|**no**  
  
In un DSN, solo la voce DRIVER è obbligatoria, ma per connettersi a un server, `sqlcmd` o `bcp` richiede il valore nella voce SERVER.  

Se è specificata la stessa opzione sia nel DSN che nella riga di comando di `sqlcmd` o di `bcp`, l'opzione della riga di comando sostituisce il valore usato nel DSN. Se ad esempio il DSN include una voce DATABASE e la riga di comando di `sqlcmd` include **-d**, viene usato il valore passato a **-d**. Se si specifica **Trusted_Connection=yes** nel DNS, viene usata l'autenticazione Kerberos e il nome utente (**-U**) e la password (**-P**), se specificati, vengono ignorati.

Gli script esistenti che richiamano `isql` possono essere modificati per l'uso di `sqlcmd` definendo l'alias seguente: `alias isql="sqlcmd -D"`.  

## <a name="see-also"></a>Vedere anche  
[Connessione a **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
