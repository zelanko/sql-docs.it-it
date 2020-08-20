---
description: Guida di riferimento a errori ed eventi (replica)
title: Guida di riferimento a errori ed eventi (replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 10d2073949de158c0773876adef0ba06d6e587eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482412"
---
# <a name="errors-and-events-reference-replication"></a>Guida di riferimento a errori ed eventi (replica)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  In questa sezione della documentazione vengono fornite informazioni sulla causa e sulla risoluzione di diversi errori correlati alla replica.  
  
|Errore|Message|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|Non è possibile inserire la riga di chiave duplicata nell'oggetto '%.*ls!' con indice univoco '%.\*ls'.|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|Violazione del vincolo %ls '%.*ls'. Non è possibile inserire la chiave duplicata nell'oggetto '%.\*ls'.|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|Il database '%ls' è stato ripristinato ma è stato rilevato un errore durante il ripristino o la rimozione della replica. Il database è stato lasciato offline. Vedere l'argomento MSSQL_ENG003165 della documentazione online di SQL Server.|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|Impossibile %S_MSG la %S_MSG '%.*ls' perché è in uso per la replica.|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|Impossibile modificare %S_MSG '%.*ls' perché è in corso di pubblicazione per la replica.|  
|MSSQL_ENG007395. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile avviare una transazione nidificata per il provider OLE DB "%ls" per il server collegato "%ls". È necessaria una transazione nidificata perché l'opzione XACT_ABORT è stata impostata su OFF.|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|Impossibile eliminare la pubblicazione. Vi è associata una sottoscrizione.|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|Il server '%s' non è definito come server di sottoscrizione.|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%s' non è configurato come server di distribuzione.|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%s' non è configurato come database di distribuzione.|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|Il database di distribuzione '%s' è associato a un server di pubblicazione. Impossibile eliminarlo.|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|Al server di distribuzione '%s' sono associati database di distribuzione. Impossibile eliminarlo.|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|Al Sottoscrittore '%s' sono associate sottoscrizioni nel database di pubblicazione '%s'. Impossibile eliminarlo.|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|Replica-%s: l'esecuzione dell'agente %s è riuscita. %s|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|Replica-%s: l'esecuzione dell'agente %s non è riuscita. %s|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|Replica-%s: ripetizione dell'esecuzione dell'agente %s pianificata. %s|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|La sottoscrizione creata dal Sottoscrittore '%s' della pubblicazione '%s' è scaduta ed è stata eliminata.|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Una o più sottoscrizioni della pubblicazione sono scadute.|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di lettura log e l'agente di distribuzione siano in esecuzione e siano in grado di rispettare i requisiti relativi alla latenza.|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di merge sia in esecuzione e sia in grado di rispettare i requisiti previsti.|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di merge sia in esecuzione e sia in grado di rispettare i requisiti previsti.|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di merge sia in esecuzione e sia in grado di rispettare i requisiti previsti.|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di merge sia in esecuzione e sia in grado di rispettare i requisiti previsti.|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|Accesso non riuscito per l'utente '%.*ls'.%.\*ls|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|A un database può connettersi un solo agente di lettura log o una sola procedura correlata ai log (sp_repldone, sp_replcmds e sp_replshowcmds) alla volta. Se è stata eseguita una procedura correlata ai log, eliminare la connessione utilizzata per eseguire la procedura oppure eseguire sp_replflush tramite tale connessione prima di avviare l'agente di lettura log o di eseguire un'altra procedura relativa ai log.|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|Nessun messaggio di stato registrato dall'agente di replica negli ultimi %ld minuti. Questa condizione può indicare che l'agente non risponde oppure che l'attività del sistema è elevata. Verificare che i record vengano replicati nella destinazione e che le connessioni al Sottoscrittore, al server di pubblicazione e al server di distribuzione siano ancora attive.|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|Arresto dell'agente. Per ulteriori informazioni, cercare nella cronologia dei processi di SQL Server Agent il processo '%s'.|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|La sottoscrizione del Sottoscrittore '%s' dell'articolo '%s' della pubblicazione '%s' è stata reinizializzata dopo un errore di convalida.|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|La sottoscrizione del Sottoscrittore '%s' dell'articolo '%s' della pubblicazione '%s' non ha superato la convalida dei dati.|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|La sottoscrizione del Sottoscrittore '%s' dell'articolo '%s' della pubblicazione '%s' ha superato la convalida dei dati.|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|L'agente anonimo può essere eliminato solo da '%s' e dai membri del ruolo db_owner.|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|Impossibile trovare la riga nel Sottoscrittore durante l'applicazione del comando replicato.|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|Lo snapshot iniziale per la pubblicazione '%s' non è ancora disponibile.|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|Lo snapshot iniziale per l'articolo '%s' non è ancora disponibile.|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|La tabella dei conflitti '%s' non esiste.|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|Impossibile creare una sottodirectory nella directory di lavoro della replica.(%1!)|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|Impossibile copiare il file script utente nel server di distribuzione.(%ls)|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|Lo snapshot non è in grado di elaborare la pubblicazione '%s', probabilmente perché sono in corso attività di modifica dello schema o di aggiunta di nuovi articoli.|  
|MSSQL_ENG021617. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile eseguire SQL*PLUS. Verificare che nel server di distribuzione sia installata una versione corrente del codice client Oracle.|  
|MSSQL_ENG021620. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|La versione di SQL*PLUS accessibile tramite la variabile di sistema Path non è aggiornata e non supporta la pubblicazione Oracle. Verificare che nel server di distribuzione sia installata una versione corrente del codice client Oracle.|  
|MSSQL_ENG021624. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile trovare il provider OLEDB Oracle registrato, OraOLEDB.Oracle, nel server di distribuzione '%s'. Verificare che nel server di distribuzione sia installata e registrata una versione corrente del provider Oracle OLEDB.|  
|MSSQL_ENG021626. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile connettersi al server di database Oracle '%s' utilizzando il provider Oracle OLEDB OraOLEDB.Oracle.|  
|MSSQL_ENG021627. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile connettersi al server di database Oracle '%s' utilizzando il provider Microsoft OLEDB MSDAORA.|  
|MSSQL_ENG021628. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile aggiornare il Registro di sistema del server di distribuzione "%s" per consentire l'esecuzione in-process del provider Oracle OLEDB OraOLEDB.Oracle con SQL Server. Verificare che l'account di accesso corrente sia autorizzato per la modifica delle chiavi del Registro di sistema di SQL Server.|  
|MSSQL_ENG021629. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Nel server di distribuzione manca la chiave del Registro di sistema CLSID che indica che il provider Oracle OLEDB OraOLEDB.Oracle è stato registrato. Verificare che il provider Oracle OLEDB sia installato e registrato nel server di distribuzione.|  
|MSSQL_ENG021642. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Per i server di pubblicazione eterogenei è necessario un server collegato. Esiste già un server collegato denominato '%s'. Rimuovere il server collegato o scegliere un nome di server di pubblicazione diverso.|  
|MSSQL_ENG021663. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Impossibile trovare una chiave primaria valida per la tabella di origine [%s].[%s].|  
|MSSQL_ENG021684. Vedere [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Le autorizzazioni associate all'account di accesso di amministratore per il server di pubblicazione Oracle '%s' non sono sufficienti.|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%s' deve essere un account di accesso di Windows valido con formato: 'COMPUTER\\Account di accesso' o 'DOMINIO\\Account di accesso'. Vedere la documentazione relativa a '%s'.|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|Per continuare è necessario aggiungere il processo di agente '%s' tramite '%s'. Vedere la documentazione relativa a '%s'.|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|Impossibile eseguire '%1' in '%2'.|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|Impossibile modificare la cronologia di generazione in '%1'. Per risolvere il problema, riavviare la sincronizzazione con la registrazione dettagliata della cronologia e specificare un file di output in cui registrare i dati.|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|Impossibile enumerare le modifiche negli articoli con filtri di riga con parametri. Se il problema persiste, aumentare il timeout per le query per questo processo, ridurre il periodo di memorizzazione per la pubblicazione e migliorare gli indici delle tabelle pubblicate.|  
  
  
