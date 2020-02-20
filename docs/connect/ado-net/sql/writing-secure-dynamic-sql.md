---
title: Scrittura di istruzioni SQL dinamiche protette in SQL Server
description: Vengono descritte le tecniche per la scrittura di istruzioni SQL dinamiche protette usando le stored procedure.
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d64b260d8d700afc8ed354d87de730e8c3b21f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253366"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>Scrittura di istruzioni SQL dinamiche protette in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L'attacco SQL injection è il processo con cui un utente malintenzionato immette istruzioni Transact-SQL anziché un input valido. Se l'input viene passato direttamente al server senza essere convalidato e se l'applicazione esegue inavvertitamente il codice inserito, è possibile che l'attacco danneggi o distrugga i dati.  
  
Per la prevenzione degli attacchi di questo tipo è necessario esaminare tutte le procedure che creano istruzioni SQL perché SQL Server esegue tutte le query sintatticamente valide che riceve. Anche i dati con parametri possono essere modificati da un utente malintenzionato abile e determinato. Se si usa SQL dinamico, assicurarsi di impostare parametri per i comandi e di non includere mai i valori dei parametri direttamente nella stringa di query.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>Anatomia di un attacco SQL injection  
Il processo di intrusione termina prematuramente una stringa di testo e aggiunge un nuovo comando. Poiché prima che venga eseguito è possibile che al comando inserito vengano aggiunte ulteriori stringhe, l'utente malintenzionato termina la stringa inserita con un contrassegno di commento "--". Al momento del'esecuzione, il testo successivo al segno di commento viene ignorato. È possibile inserire più comandi usando un punto e virgola (;) come delimitatore.  
  
Se il codice SQL inserito è sintatticamente corretto, le manomissioni non possono essere rilevate a livello di programmazione. È pertanto necessario convalidare tutti gli input utente e rivedere attentamente il codice per l'esecuzione dei comandi SQL generati nel server in uso. Non eseguire mai la concatenazione di input utente non convalidato. La concatenazione delle stringhe è il punto di ingresso principale per l'attacco intrusivo nel codice script.  
  
Di seguito sono riportate alcune linee guida utili:  
  
- Non compilare mai istruzioni Transact-SQL direttamente dall'input dell'utente, ma usare le stored procedure per convalidare tale input.  
  
- Convalidare sempre gli input utente testando tipo, lunghezza, formato e intervallo. Usare la funzione Transact-SQL QUOTENAME() per aggiungere un carattere di escape ai nomi di sistema o la funzione REPLACE() per aggiungerlo a qualsiasi carattere di una stringa.  
  
- Implementare più livelli di convalida in ogni livello dell'applicazione.  
  
- Testare le dimensioni e il tipo di dati dell'input e imporre limiti appropriati. In questo modo è possibile impedire intenzionali sovraccarichi del buffer.  
  
- Testare il contenuto delle variabili stringa e accettare solo i valori previsti. Rifiutare voci contenenti dati binari, sequenze di escape e caratteri di commento.  
  
- Quando si utilizzano documenti XML, convalidare tutti i dati in base al relativo schema man mano che vengono immessi.  
  
- In ambienti multilivello è necessario convalidare tutti i dati prima di consentirne l'inserimento in aree attendibili.  
  
- Non accettare le stringhe seguenti nei campi da cui è possibile costruire i nomi di file: AUX, CLOCK$, da COM1 a COM8, CON, CONFIG$, da LPT1 a LPT8, NUL e PRN.  
  
- Usare gli oggetti <xref:Microsoft.Data.SqlClient.SqlParameter> con stored procedure e comandi per specificare il controllo del tipo e la convalida della lunghezza.  
  
- Usare le espressioni <xref:System.Text.RegularExpressions.Regex> nel codice client per filtrare i caratteri non validi.  
  
## <a name="dynamic-sql-strategies"></a>Strategie di SQL dinamico  
L'esecuzione di istruzioni SQL create in modo dinamico nel codice procedurale interrompe la catena di proprietà e fa in modo che SQL Server controlli le autorizzazioni del chiamante per gli oggetti a cui si accede con SQL dinamico.  
  
SQL Server include metodi per concedere agli utenti l'accesso ai dati usando stored procedure e funzioni definite dall'utente che eseguono istruzioni SQL dinamiche.  
  
- L'uso della rappresentazione con la clausola EXECUTE AS Transact-SQL.  
  
- Firma di stored procedure con certificati.  
  
### <a name="execute-as"></a>EXECUTE AS  
La clausola EXECUTE AS sostituisce le autorizzazioni del chiamante con quelle dell'utente specificato nella clausola EXECUTE AS. Le stored procedure o i trigger nidificati vengono eseguiti nel contesto di sicurezza dell'utente proxy. Questo può interrompere le applicazioni che si basano sulla sicurezza a livello di riga o richiedono il controllo. Alcune funzioni che restituiscono l'identità dell'utente restituiscono l'utente specificato nella clausola EXECUTE AS, non il chiamante originale. Il contesto di esecuzione viene di nuovo assegnato al chiamante originale solo dopo l'esecuzione della procedura o quando viene generata un'istruzione REVERT.  
  
### <a name="certificate-signing"></a>Firma del certificato  
Quando viene eseguita una stored procedure firmata con un certificato le autorizzazioni concesse all'utente del certificato vengono unite a quelle del chiamante. Il contesto di esecuzione rimane lo stesso: l'utente del certificato non rappresenta il chiamante. La firma delle stored procedure richiede l'esecuzione di alcuni passaggi. Ogni volta che la procedura viene modificata, deve essere nuovamente firmata.  
  
### <a name="cross-database-access"></a>Accesso tra database  
Il concatenamento della proprietà tra database non funziona nei casi in cui vengono eseguite istruzioni SQL create in modo dinamico. Per aggirare questo problema, in SQL Server è possibile creare un stored procedure che accede ai dati di un altro database e firmare la procedura con un certificato disponibile in entrambi i database. In questo modo gli utenti possono accedere alle risorse di database usate dalla procedura senza che sia necessario concedere loro l'accesso al database o le autorizzazioni.  
  
## <a name="external-resources"></a>Risorse esterne  
Per ulteriori informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[Stored procedure](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md) e [SQL injection](../../../relational-databases/security/sql-injection.md) nella documentazione online di SQL Server|Gli argomenti descrivono come creare le stored procedure e come funziona un attacco SQL injection.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Scenari di sicurezza delle applicazioni in SQL Server](application-security-scenarios-sql-server.md)
