---
title: Compatibilità di FileTable con altre funzionalità di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ab7963d83937c3572363ea921724cefb8b4adff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920795"
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>Compatibilità di FileTable con altre funzionalità di SQL Server
  Viene descritto il funzionamento delle tabelle FileTable con altre funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="alwayson"></a> Gruppi di disponibilità AlwaysOn e tabelle FileTable  
 Quando il database che contiene dati FILESTREAM o FileTable appartiene a un gruppo di disponibilità AlwaysOn:  
  
-   La funzionalità FileTable è supportata parzialmente dai [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Dopo un failover, i dati FileTable sono accessibili nella replica primaria, ma non nelle repliche secondarie leggibili.  
  
    > [!NOTE]  
    >  Si noti che dopo un failover, tutte le funzionalità FILESTREAM sono supportate. I dati FILESTREAM sono accessibili sia nelle repliche secondarie leggibili sia nella nuova primaria.  
  
-   Le funzioni FILESTREAM e FileTable accettano o restituiscono nomi di rete virtuale anziché nomi computer. Per altre informazioni su queste funzioni, vedere [Funzioni FileStream e FileTable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql).  
  
-   Ogni accesso a dati FILESTREAM o FileTable tramite le API del file system deve utilizzare VNN anziché nomi computer. Per altre informazioni, vedere [FILESTREAM e FileTable con i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
##  <a name="OtherPartitioning"></a> Partizionamento e tabelle FileTable  
 Il partizionamento non è supportato nelle tabelle FileTable. Con il supporto per più filegroup FILESTREAM, è possibile gestire i problemi di scalabilità verticale puri senza dovere ricorrere al partizionamento nella maggior parte degli scenari (a differenza di FILESTREAM SQL 2008).  
  
##  <a name="OtherRepl"></a> Replica e tabelle FileTable  
 La replica e le funzionalità correlate, quali replica transazionale, replica di tipo merge, Change Data Capture e rilevamento delle modifiche, non sono supportate con le tabelle FileTable.  
  
##  <a name="OtherIsolation"></a> Semantica delle transazioni e tabelle FileTable  
 **applicazioni Windows**  
 Poiché le applicazioni di Windows non riconoscono le transazioni di database, le operazioni di scrittura di Windows non forniscono le proprietà ACID di una transazione di database. I rollback transazionali e il recupero, pertanto, non sono possibili con operazioni di aggiornamento di Windows.  
  
 **Applicazioni Transact-SQL**  
 Per le applicazioni TSQL eseguite nella colonna FILESTREAM (file_stream) in una tabella FileTable, la semantica dell'isolamento è la stessa utilizzata con il tipo di dati FILESTREAM in una normale tabella utente.  
  
##  <a name="OtherQueryNot"></a> Notifica delle query e tabelle FileTable  
 La query non può contenere un riferimento alla colonna FILESTREAM nella tabella FileTable, nella clausola WHERE o in qualunque altra parte della query.  
  
##  <a name="OtherSelectInto"></a> SELECT INTO e tabelle FileTable  
 le istruzioni SELECT INTO da una tabella FileTable non propagheranno la semantica della tabella FileTable nella tabella di destinazione creata (come le colonne FILESTREAM in una normale tabella). Tutte le colonne della tabella di destinazione si comporteranno proprio come normali colonne. A tali colonne non sarà associata alcuna semantica della tabella FileTable.  
  
##  <a name="OtherTriggers"></a> Trigger e tabelle FileTable  
 **Trigger DDL (Data Definition Language)**  
 Non vi sono considerazioni speciali relative ai trigger DDL con tabelle FileTable. Verranno attivati normali trigger DDL per operazioni di creazione/modifica del database, nonché per operazioni CREATE/ALTER TABLE per le tabelle FileTable. I trigger possono recuperare i dati evento effettivi, che includono il testo del comando DDL e altre informazioni, chiamando la funzione EVENTDATA(). Non vi sono nuovi eventi o modifiche per lo schema Eventdata esistente.  
  
 **Trigger DML (Data Manipulation Language)**  
 Queste restrizioni verranno applicate durante l'operazione DDL per creare trigger.  
  
-   Le tabelle FileTable NON supporteranno trigger INSTEAD OF per operazioni DML. Si tratta di una restrizione esistente per tutte le tabelle che contengono colonne FILESTREAM.  
  
-   Le tabelle FileTable NON supporteranno trigger AFTER per operazioni DML.  
  
-   I trigger definiti in una tabella FileTable non sono in grado di aggiornare alcuna tabella FileTable (inclusa la tabella FileTable padre). Questa restrizione ha come principale obiettivo di impedire che un trigger crei un conflitto di blocco con i blocchi controllati dall'accesso al file system nella stessa transazione.  
  
 **Accesso non transazionale e relativi effetti sui trigger**  
 -   Quando in un database è consentito l'accesso non transazionale per l'aggiornamento, è possibile eseguire un aggiornamento sul posto dei dati FILESTREAM in qualsiasi tabella, inclusa la tabella FileTable del database. Grazie a questa possibilità, l'immagine precedente del contenuto di FILESTREAM potrebbe non essere disponibile per l'utilizzo da parte del trigger.  
  
-   Per operazioni di aggiornamento non transazionali tramite file system, in SQL Server verrà creata una transazione interna per acquisire l'operazione CloseHandle e sarà possibile attivare qualsiasi trigger DML definito come parte di tale transazione. Benché non impedito, un rollback, ad esempio una transazione all'interno del corpo del trigger, non consente di eseguire il rollback delle modifiche apportate a FILESTREAM.  Tale operazione di rollback può inoltre impedire l'attivazione dei trigger UPDATE, anche qualora il contenuto di FILESTREAM sia stato modificato.  
  
-   Oltre a questi effetti, per i trigger nelle tabelle FileTable è necessario gestire altri due comportamenti:  
  
    -   In caso di operazioni di aggiornamento non transazionali nella tabella FileTable tramite il file system, è possibile che il contenuto di FILESTREAM venga bloccato in modo esclusivo da altre operazioni Win32 e non sia accessibile per operazioni di lettura/scrittura tramite il corpo del trigger. In tali casi, qualsiasi tentativo di accedere al contenuto di FILESTREAM all'interno del corpo del trigger può generare un errore di violazione della condivisione. È opportuno progettare i trigger in modo che siano in grado di gestire tali errori in modo appropriato.  
  
    -   L'immagine AFTER di FILESTREAM può non essere stabile, perché in alcuni casi può essere contemporaneamente soggetta a scrittura da parte di altri aggiornamenti non transazionali, a causa delle modalità di condivisione consentite nell'accesso al file system.  
  
-   L'arresto anomalo di handle Win32, ad esempio la terminazione esplicita di handle Win32 effettuata da un amministratore OPPURE a causa di un arresto del database, provocherà la mancata esecuzione dei trigger utente durante le operazioni di recupero, anche qualora il contenuto di FILESTREAM sia stato modificato dall'applicazione Win32 arrestata in modo anomalo.  
  
##  <a name="OtherViews"></a> Viste e tabelle FileTable  
 **Viste**  
 È possibile creare una vista in una tabella FileTable come in qualsiasi altra tabella. A una vista creata in una tabella FileTable, tuttavia, si applicano le considerazioni seguenti:  
  
-   Nella vista non sarà disponibile alcuna semantica FileTable, ad esempio il comportamento delle colonne nella vista, incluse le colonne degli attributi dei file, sarà quello di normali colonne della vista senza alcuna semantica speciale. Lo stesso vale per le righe che rappresentano file/directory.  
  
-   La vista potrebbe essere aggiornabile in base alla semantica delle viste aggiornabili, ma i vincoli di tabella sottostanti possono rifiutare gli aggiornamenti come nella tabella.  
  
-   È possibile visualizzare il percorso per un file nella vista aggiungendolo come colonna esplicita nella vista. Ad esempio:   
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, ..., GetFileNamespacePath() AS PATH, column3,...  FROM Documents`  
  
 **Viste indicizzate**  
 Attualmente le viste indicizzate non possono includere colonne FILESTREAM o colonne calcolate/calcolate persistenti che dipendono dalle colonne FILESTREAM. Questo comportamento è lo stesso anche per le viste definite nella tabella FileTable.  
  
##  <a name="OtherSnapshots"></a> Isolamento dello snapshot e tabelle FileTable  
 L'isolamento dello snapshot e l'isolamento dello snapshot Read Committed si basano sulla possibilità di disporre di uno snapshot dei dati per i lettori, anche quando vengono eseguite operazioni di aggiornamento sui dati. Le tabelle FileTable, tuttavia, consentono l'accesso in scrittura non transazionale ai dati FILESTREAM. Di conseguenza, sussistono le restrizioni seguenti per l'utilizzo di queste funzionalità in database che contengono tabelle FileTable:  
  
-   Un database che contiene tabelle FileTable può essere modificato per abilitare l'isolamento dello snapshot e/o l'isolamento dello snapshot Read Committed.  
  
-   Quando l'accesso non transazionale è impostato su FULL per il database, una transazione eseguita in isolamento dello snapshot o isolamento dello snapshot Read Committed ha il comportamento seguente:  
  
    -   Non viene completata alcuna lettura [!INCLUDE[tsql](../../../includes/tsql-md.md)] della colonna file_stream della tabella FileTable. È comunque possibile eseguire operazioni INSERT e UPDATE nella colonna, ma solo se la lettura non viene effettuata dalla colonna file_stream.  
  
    -   Se l'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] specifica hint di tabella READCOMMITTEDLOCK, le letture vengono completate e consentiranno l'utilizzo di blocchi sulle righe anziché l'utilizzo del controllo delle versioni delle righe.  
  
    -   Anche l'apertura transazionale della tabella FileTable Win32 non verrà completata.  
  
    -   L'accesso Win32 non in transazioni alla tabella FileTable viene effettuato correttamente. Tutte le query interne eseguite dalla tabella FileTable non saranno interessate.  
  
    -   L'indicizzazione full-text viene sempre completata, indipendentemente dalle opzioni di database (READ_COMMITTED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION).  
  
##  <a name="readsec"></a> Database secondari leggibili  
 Ai database secondari leggibili si applicano le stesse considerazioni degli snapshot, come descritto nella sezione precedente, [Isolamento dello snapshot e tabelle FileTable](#OtherSnapshots).  
  
##  <a name="CDB"></a> Database indipendenti e tabelle FileTable  
 La funzionalità FILESTREAM da cui dipende la funzionalità FileTable richiede alcuni interventi di configurazione all'esterno del database. Pertanto un database in cui si utilizza FILESTREAM o FileTable non è completamente indipendente.  
  
 È possibile impostare l'indipendenza del database su PARTIAL se si desidera utilizzare alcune funzionalità dei database indipendenti, ad esempio gli utenti indipendenti. In tal caso, tuttavia, è necessario tenere presente che alcune impostazioni del database non sono contenute nel database e non vengono spostate automaticamente quando viene spostato il database.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle FileTable](manage-filetables.md)  
  
  
