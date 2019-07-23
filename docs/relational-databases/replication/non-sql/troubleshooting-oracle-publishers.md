---
title: Risoluzione dei problemi dei server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3edd60a47ac4cebcdea3f70a0658ce837e3d63ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095652"
---
# <a name="troubleshooting-oracle-publishers"></a>Risoluzione dei problemi dei server di pubblicazione Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento vengono elencati alcuni problemi che possono verificarsi durante la configurazione e l'uso di un server di pubblicazione Oracle.  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>Viene generato un errore relativo al software di rete e client Oracle  
 L'account con cui viene eseguito [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel server di distribuzione deve disporre di autorizzazioni di lettura ed esecuzione per la directory e tutte le sottodirectory in cui è installato il software di rete client Oracle. Se tali autorizzazioni non vengono concesse o i componenti client Oracle non sono installati correttamente, verrà visualizzato il messaggio di errore seguente:  
  
 "Impossibile connettersi al server con [provider Microsoft OLE DB per Oracle]. Impossibile trovare il client e i componenti di rete Oracle. Tali componenti vengono forniti da Oracle Corporation e fanno parte dell'installazione del software client Oracle versione 7.3.3 o successive. Se non si installano tali componenti, non sarà possibile utilizzare questo provider."  
  
 Se nel server di distribuzione è installato un client Oracle appropriato, assicurarsi che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sia stato arrestato e riavviato al termine dell'installazione del client. Questa operazione è necessaria affinché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] riconosca i componenti del client.  
  
 Se l'errore persiste nonostante siano state verificate la concessione delle autorizzazioni e la corretta installazione dei componenti, verificare che le impostazioni del Registro di sistema in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI siano corrette.  
  
-   Impostazioni corrette per Oracle 10g:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Impostazioni corrette per Oracle 9i:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>Il server di distribuzione SQL Server non è in grado di connettersi all'istanza del database Oracle  
 Se il server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non è in grado di connettersi al server di pubblicazione Oracle, verificare le condizioni seguenti:  
  
-   Nel server di distribuzione è installato il software Oracle necessario.  
  
-   Il database Oracle è online ed è possibile connettersi a tale database mediante uno strumento come SQL*Plus.  
  
-   L'account di accesso utilizzato nella replica per la connessione al server di pubblicazione Oracle dispone di autorizzazioni sufficienti. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
-   I nomi TNS definiti durante la configurazione del server di pubblicazione Oracle sono elencati nel file tnsnames.ora.  
  
-   Vengono utilizzati i valori corretti di percorso e Oracle Home. Anche in caso di installazione di un solo set di file binari Oracle nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , assicurarsi che le variabili di ambiente relative a Oracle Home siano state impostate correttamente. Se le variabili di ambiente vengono modificate, per rendere effettiva la modifica è necessario arrestare e riavviare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni sulla configurazione e sul test della connettività, vedere la sezione relativa all'installazione e alla configurazione del software di rete client Oracle nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>Il server di pubblicazione Oracle è associato a un altro server di distribuzione  
 Un server di pubblicazione Oracle può essere associato soltanto a un server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se al server di pubblicazione Oracle è associato un diverso server di distribuzione, questo deve essere eliminato per poterne utilizzare un altro. Se non viene innanzitutto eliminato il server di distribuzione, verrà visualizzato uno dei messaggi di errore seguenti:  
  
-   "L'istanza del server Oracle '\<*NomeServerPubblicazioneOracle*>' è stata precedentemente configurata per l'uso di '\<*NomeDatabaseDistribuzioneSQLServer*>' come database di distribuzione. Per iniziare a usare '\<*NuovoDatabaseDistribuzioneSQLServer*>' come database di distribuzione, è necessario rimuovere la configurazione corrente della replica nell'istanza del server Oracle, eliminando così tutte le pubblicazioni presenti in tale istanza del server."  
  
-   "Il server Oracle '\<*NomeServerOracleServer*>' è già definito come server di pubblicazione '\<*NomeServerPubblicazioneOracle*>' nel database di distribuzione '\<*NomeDatabaseDistribuzioneSQL*>. *\<NomeDatabaseDistribuzione>* '. Eliminare il server di pubblicazione oppure eliminare il sinonimo public ' *\<NomeSinonimo*' per ricrearlo."  
  
 Con l'eliminazione di un server di pubblicazione Oracle, vengono automaticamente rimossi gli oggetti di replica nel database Oracle. In alcuni casi è tuttavia necessario eseguire manualmente la pulizia degli oggetti di replica Oracle. Per rimuovere manualmente gli oggetti di replica Oracle creati con la replica:  
  
1.  Connettersi al server di pubblicazione Oracle con autorizzazioni DBA.  
  
2.  Eseguire il comando SQL `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`.  
  
3.  Eseguire il comando SQL `DROP USER <replication_administrative_user_schema>``CASCADE;`.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>Viene generato l'errore SQL Server 21663 relativo alla mancanza di una chiave primaria  
 Gli articoli delle pubblicazioni transazionali devono disporre di una chiave primaria valida. In assenza di una chiave primaria valida, quando si tenta di aggiungere un articolo viene visualizzato il messaggio di errore seguente:  
  
 "Impossibile trovare una chiave primaria valida per la tabella di origine [\<*ProprietarioTabella*>].[\<*NomeTabella*>]"  
  
 Per informazioni sui requisiti delle chiavi primarie, vedere la sezione relativa a vincoli e indici univoci nell'argomento [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>Viene generato l'errore SQL Server 21642 relativo all'accesso a un server collegato duplicato  
 Durante la configurazione iniziale di un server di pubblicazione Oracle, viene creata una voce di server collegato per la connessione tra server di pubblicazione e server di distribuzione. Il nome del server collegato corrisponde al nome del servizio TNS Oracle. Se si tenta di creare un server collegato con lo stesso nome, viene visualizzato il messaggio di errore seguente:  
  
 'Per i server di pubblicazione eterogenei è necessario un server collegato. Esiste già un server collegato denominato ' *\<NomeServerCollegato*'. Rimuovere il server collegato o scegliere un nome di server di pubblicazione diverso'.  
  
 Questo errore si può verificare se si tenta di creare il server collegato direttamente oppure se è stata precedentemente eliminata la relazione tra il server di pubblicazione Oracle e il server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e si tenta ora di riconfigurarla. Se questo errore viene visualizzato durante un tentativo di riconfigurazione del server di pubblicazione, eliminare il server collegato con [sp_dropserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md).  
  
 Se è necessario connettersi al server di pubblicazione Oracle tramite una connessione al server collegato, creare un altro nome di servizio TNS e quindi usare tale nome nella chiamata a [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Per informazioni sulla creazione di nomi di servizio TNS, vedere la documentazione Oracle.  
  
## <a name="sql-server-error-21617-is-raised"></a>Viene generato l'errore SQL Server 21617  
 La pubblicazione Oracle utilizza l'applicazione Oracle SQL*PLUS per scaricare il pacchetto del codice di supporto del server di pubblicazione nel database Oracle. Prima di tentare la configurazione del server di pubblicazione Oracle, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verifica che SQL\*PLUS sia accessibile attraverso il percorso di sistema sul database di distribuzione. Se non è possibile caricare SQL\*PLUS, verrà visualizzato il messaggio di errore seguente:  
  
 "Impossibile eseguire SQL*PLUS. Verificare che nel server di distribuzione sia installata una versione corrente del codice client Oracle."  
  
 Tentare di individuare SQL\*PLUS sul database di distribuzione. Per un'installazione client Oracle 10g, il nome del file eseguibile è sqlplus.exe. In genere, il percorso di installazione è %ORACLE_HOME%/bin. Per verificare che il percorso di SQL\*PLUS sia incluso nel percorso di sistema, esaminare il valore della variabile di sistema **Path**:  
  
1.  Fare clic con il pulsante destro del mouse su **Risorse del computer**e quindi scegliere **Proprietà**.  
  
2.  Selezionare la scheda **Avanzate** e quindi fare clic sul pulsante **Variabili d'ambiente**.  
  
3.  Nella finestra di dialogo **Variabili d'ambiente** selezionare la variabile **Path** nell'elenco **Variabili di sistema** e quindi fare clic su **Modifica**.  
  
4.  Nella finestra di dialogo **Modifica variabile di sistema** , se il percorso della cartella in cui si trova sqlplus.exe non è visualizzato nella casella di testo **Valore variabile** , modificare la stringa per includerlo.  
  
5.  Fare clic su **OK** in ogni finestra di dialogo aperta per chiuderla e salvare le modifiche.  
  
 Se non è possibile individuare sqlplus.exe sul server di distribuzione, installare una versione aggiornata del software client Oracle sul server di distribuzione. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="sql-server-error-21620-is-raised"></a>Viene generato l'errore SQL Server 21620  
 Se si esegue la connessione a un database Oracle di versione precedente alla 8.1, per la pubblicazione Oracle è necessario che il software client Oracle installato nel server di distribuzione sia di versione 9 o successiva. Se si esegue la connessione a un database Oracle di versione 8.1 o successiva, è consigliabile utilizzare software client Oracle di versione 10 o successiva.  
  
 Prima di tentare la configurazione del server di pubblicazione Oracle, la pubblicazione Oracle verifica che la versione di SQL*PLUS accessibile tramite il percorso di sistema sul server di distribuzione sia 9 o successiva. In caso contrario, verrà visualizzato il messaggio di errore seguente:  
  
 "La versione di SQL*PLUS accessibile tramite la variabile di sistema Path non è aggiornata e non supporta la pubblicazione Oracle. Verificare che nel server di distribuzione sia installata una versione corrente del codice client Oracle."  
  
 Se sul server di distribuzione sono installate più versioni del software client Oracle, verificare che la versione più recente corrisponda alla 9 e che la variabile di sistema Path faccia innanzitutto riferimento a questa versione (possono essere presenti anche i riferimenti alle altre versioni, a condizione che il riferimento alla versione più recente appaia per primo). Per ulteriori informazioni sulla modifica della variabile di sistema Path, vedere la sezione "Viene generato l'errore SQL Server 21617" più indietro in questo argomento.  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>Viene generato l'errore SQL Server 21624 o 21629  
 Per i server di distribuzione a 64 bit, la pubblicazione Oracle utilizza il provider Oracle OLEDB per Oracle (OraOLEDB.Oracle). Verificare che il provider Oracle OLEDB sia installato e registrato nel server di distribuzione. In caso contrario, uno o entrambi i messaggi di errore seguenti verranno visualizzati:  
  
-   "Impossibile trovare il provider OLEDB Oracle registrato, OraOLEDB.Oracle, nel server di distribuzione '%s'. Verificare che nel server di distribuzione sia installata e registrata una versione corrente del provider Oracle OLEDB."  
  
-   "Nel server di distribuzione manca la chiave del Registro di sistema CLSID che indica che il provider Oracle OLEDB OraOLEDB.Oracle è stato registrato. Verificare che il provider Oracle OLEDB sia installato e registrato nel server di distribuzione."  
  
 Se si utilizza il software client Oracle versione 10g, il provider è OraOLEDB10.dll, mentre per la versione 9i è OraOLEDB.dll. Il provider viene installato in %ORACLE_HOME%\BIN (ad esempio, C:\oracle\product\10.1.0\Client_1\bin). Se si scopre che il provider Oracle OLEDB non è installato sul server di distribuzione, installarlo utilizzando l'apposito disco di installazione fornito da Oracle. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 Se il provider Oracle OLEDB è installato, verificare che sia registrato. Per registrare la DLL del provider, eseguire il comando seguente dalla directory in cui è installata la DLL e quindi arrestare e riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  `regsvr32 OraOLEDB10.dll` o `regsvr32 OraOLEDB.dll`.  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>Viene generato l'errore SQL Server 21626 o 21627  
 Per verificare che l'ambiente di pubblicazione Oracle sia configurato correttamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenta di connettersi al server di pubblicazione Oracle con le credenziali di accesso specificate durante la configurazione. Se tramite il server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non è possibile connettersi al server di pubblicazione Oracle, verrà visualizzato il messaggio di errore seguente:  
  
-   "Impossibile connettersi al server di database Oracle '%s' utilizzando il provider Oracle OLEDB OraOLEDB.Oracle".  
  
 Se viene visualizzato questo messaggio di errore, verificare la connettività al database Oracle eseguendo direttamente SQL*PLUS utilizzando lo stesso account di accesso e la stessa password specificati durante la configurazione del server di pubblicazione Oracle. Per ulteriori informazioni, vedere la sezione "Il server di distribuzione SQL Server non è in grado di connettersi all'istanza del database Oracle" più indietro in questo argomento.  
  
## <a name="sql-server-error-21628-is-raised"></a>Viene generato l'errore SQL Server 21628  
 Per i server di distribuzione a 64 bit, la pubblicazione Oracle utilizza il provider Oracle OLEDB per Oracle (OraOLEDB.Oracle). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di creare una voce nel Registro di sistema che permette l'esecuzione in-process del provider Oracle con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se si verifica un problema durante la lettura o la scrittura della voce del Registro di sistema, verrà visualizzato il messaggio di errore seguente:  
  
 "Impossibile aggiornare il Registro di sistema del server di distribuzione '%s' per consentire l'esecuzione in-process del provider Oracle OLEDB OraOLEDB.Oracle con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Verificare che l'account di accesso corrente sia autorizzato per la modifica delle chiavi del Registro di sistema di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per la pubblicazione Oracle è necessario che la voce del Registro di sistema esista e che sia impostata su **1** per i server di distribuzione a 64 bit. Se la voce non esiste, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenterà di crearla. Se la voce esiste ma è impostata su **0**, l'impostazione non verrà modificata e la configurazione del server di pubblicazione Oracle Publisher avrà esito negativo.  
  
 Per visualizzare e modificare l'impostazione nel Registro di sistema:  
  
1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**.  
  
2.  Nella finestra di dialogo **Esegui** digitare **regedit**e quindi fare clic su **OK**.  
  
3.  Individuare HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\ *\<NomeIstanza>* \Providers.  
  
     Nella cartella Providers dovrebbe essere presente una cartella denominata OraOLEDB.Oracle. In questa cartella dovrebbe essere incluso il nome valore DWORD **AllowInProcess**, con un valore pari a **1**.  
  
4.  Se **AllowInProcess** è impostato su **0**, aggiornare la voce del Registro di sistema su **1**:  
  
    1.  Fare clic con il pulsante destro del mouse sulla voce e quindi scegliere **Modifica**.  
  
    2.  Nella finestra di dialogo **Modifica stringa** immettere **1** nel campo **Dati valore** .  
  
## <a name="sql-server-error-21684-is-raised"></a>Viene generato l'errore SQL Server 21684  
 Se l'account utente di amministrazione non dispone di privilegi sufficienti, verrà visualizzato il messaggio di errore seguente:  
  
 "Le autorizzazioni associate all'account di accesso di amministratore per il server di pubblicazione Oracle '%s' non sono sufficienti."  
  
 Per verificare le autorizzazioni assegnate all'utente, eseguire la query `SELECT * from session_privs`. L'output avrà un aspetto analogo al seguente:  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>Vengono riscontrati problemi relativi alle autorizzazioni per lo schema utente di replica  
 Lo schema utente di replica deve disporre delle autorizzazioni descritte nella sezione relativa alla creazione manuale dello schema utente in [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="oracle-error-ora-01000"></a>Errore Oracle ORA-01000  
 Durante il processo di aggiunta di articoli a una pubblicazione, nella replica vengono utilizzati cursori sul server di pubblicazione Oracle. Durante questo processo è possibile superare il numero massimo dei cursori disponibili sul server di pubblicazione. In questo caso, viene generato l'errore seguente:  
  
 "ORA-01000: maximum open cursors exceeded"  
  
 Per evitare questo problema, verificare che l'impostazione **max_open_cursors** dei database Oracle sia impostata su un numero sufficientemente elevato (almeno 1000). Per ulteriori informazioni su questa impostazione, vedere la documentazione Oracle.  
  
## <a name="oracle-error-ora-01555"></a>Errore Oracle ORA-01555  
 L'errore di database Oracle seguente non è correlato alla replica snapshot, bensì al modo in cui Oracle costruisce viste di dati con consistenza in lettura:  
  
 "ORA-01555: Snapshot too old"  
  
 Utilizzando oggetti noti come segmenti di rollback, Oracle costruisce viste di dati con consistenza in lettura relativamente al momento in cui è stata eseguita un'istruzione SQL. L'errore "snapshot too old" può verificarsi in caso di sovrascrittura delle informazioni di rollback da parte di altre sessioni simultanee. Nelle versioni precedenti a Oracle 9i, il metodo consigliato per ridurre la frequenza di questo errore consiste nell'incrementare le dimensioni e/o il numero dei segmenti di rollback e assegnare transazioni estese a uno specifico segmento di rollback.  
  
 In Oracle 9i, Oracle ha introdotto il concetto di spazio di tabella UNDO, che sostituisce il segmento di rollback. Per evitare l'errore "snapshot too old" in Oracle 9i, è consigliabile:  
  
-   Creare uno spazio di tabella UNDO con una quantità appropriata di spazio disponibile.  
  
-   Impostare la garanzia di memorizzazione per lo spazio di tabella (Oracle 10G e versioni successive).  
  
-   Configurare i parametri di inizializzazione Oracle UNDO_MANAGEMENT e UNDO_RETENTION.  
  
 Per informazioni dettagliate su come evitare l'errore "snapshot too old", vedere la documentazione Oracle.  
  
## <a name="oracle-error-ora-22285"></a>Errore Oracle ORA-22285  
 Se in una tabella è inclusa una colonna BFILE, i dati per la colonna vengono archiviati nel file system. All'account utente di amministrazione della replica deve essere concesso l'accesso alla directory in cui sono archiviati i dati mediante la sintassi seguente:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Se l'accesso non viene concesso, l'agente di lettura log genera l'errore seguente:  
  
 "ORA-22285: non-existent directory or file for FILEOPEN operation"  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>Le modifiche apportate richiedono la riconfigurazione del server di pubblicazione  
 Le modifiche apportate a procedure o tabelle di metadati della replica richiedono l'eliminazione e la riconfigurazione del server di pubblicazione. Per riconfigurare il server di pubblicazione, è necessario eliminarlo ed eseguirne nuovamente la configurazione mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL o RMO. Per informazioni sulla configurazione del server di pubblicazione, vedere [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 **Per eliminare un server di pubblicazione Oracle (** SQL Server Management Studio **)**  
  
1.  Connettersi al server di distribuzione per il server di pubblicazione Oracle in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ed espandere il nodo del server.  
  
2.  Fare clic con il pulsante destro del mouse su **Replica**e quindi scegliere **Proprietà server di distribuzione**.  
  
3.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione** deselezionare la casella di controllo per il server di pubblicazione Oracle.  
  
4.  Fare clic su **OK**.  
  
 **Per eliminare un server di pubblicazione Oracle (Transact-SQL)**  
  
-   Eseguire **sp_dropdistpublisher**. Per altre informazioni, vedere [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
