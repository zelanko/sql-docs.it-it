---
title: Scrittura di istruzioni SQL dinamiche protette in SQL Server
description: Vengono descritte le tecniche per la scrittura di codice SQL dinamico sicuro tramite stored procedure.
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: dd7b76e3333d51a94d6f215a6608511629f35fbe
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451867"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>Scrittura di istruzioni SQL dinamiche protette in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL injection è il processo mediante il quale un utente malintenzionato immette istruzioni Transact-SQL anziché un input valido. Se l'input viene passato direttamente al server senza essere convalidato e se l'applicazione esegue inavvertitamente il codice inserito, è possibile che l'attacco danneggi o distrugga i dati.  
  
Per la prevenzione degli attacchi di questo tipo è necessario esaminare tutte le procedure che creano istruzioni SQL perché SQL Server esegue tutte le query sintatticamente valide che riceve. Anche i dati con parametri possono essere modificati da un utente malintenzionato abile e determinato. Se si usa SQL dinamico, assicurarsi di parametrizzare i comandi e non includere mai i valori dei parametri direttamente nella stringa di query.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>Anatomia di un attacco SQL injection  
Il processo di intrusione termina prematuramente una stringa di testo e aggiunge un nuovo comando. Poiché prima che venga eseguito è possibile che al comando inserito vengano aggiunte ulteriori stringhe, l'utente malintenzionato termina la stringa inserita con un contrassegno di commento "--". Al momento del'esecuzione, il testo successivo al segno di commento viene ignorato. È possibile inserire più comandi usando un punto e virgola (;) delimitatore.  
  
Se il codice SQL inserito è sintatticamente corretto, le manomissioni non possono essere rilevate a livello di programmazione. È pertanto necessario convalidare tutti gli input utente e rivedere attentamente il codice per l'esecuzione dei comandi SQL generati nel server in uso. Non eseguire mai la concatenazione di input utente non convalidato. La concatenazione delle stringhe è il punto di ingresso principale per l'attacco intrusivo nel codice script.  
  
Ecco alcune linee guida utili:  
  
- Non compilare mai istruzioni Transact-SQL direttamente dall'input dell'utente; utilizzare le stored procedure per convalidare l'input dell'utente.  
  
- Convalidare sempre gli input utente testando tipo, lunghezza, formato e intervallo. Utilizzare la funzione Transact-SQL QUOTEname () per eseguire l'escape dei nomi di sistema o la funzione REPLACE () per eseguire l'escape di qualsiasi carattere di una stringa.  
  
- Implementare più livelli di convalida in ogni livello dell'applicazione.  
  
- Testare le dimensioni e il tipo di dati dell'input e imporre limiti appropriati. In questo modo è possibile impedire intenzionali sovraccarichi del buffer.  
  
- Testare il contenuto delle variabili stringa e accettare solo i valori previsti. Rifiutare voci contenenti dati binari, sequenze di escape e caratteri di commento.  
  
- Quando si utilizzano documenti XML, convalidare tutti i dati in base al relativo schema man mano che vengono immessi.  
  
- In ambienti multilivello è necessario convalidare tutti i dati prima di consentirne l'inserimento in aree attendibili.  
  
- Non accettare le stringhe seguenti in campi da cui è possibile creare nomi di file: AUX, CLOCK$, da COM1 a COM8, CON, CONFIG$, da LPT1 a LPT8, NUL e PRN.  
  
- Utilizzare <xref:Microsoft.Data.SqlClient.SqlParameter> oggetti con stored procedure e comandi per fornire il controllo del tipo e la convalida della lunghezza.  
  
- Usare espressioni <xref:System.Text.RegularExpressions.Regex> nel codice client per filtrare i caratteri non validi.  
  
## <a name="dynamic-sql-strategies"></a>Strategie SQL dinamiche  
L'esecuzione di istruzioni SQL create in modo dinamico nel codice procedurale interrompe la catena di proprietà, causando SQL Server controllare le autorizzazioni del chiamante sugli oggetti a cui si accede tramite SQL dinamico.  
  
SQL Server include metodi per concedere agli utenti l'accesso ai dati usando stored procedure e funzioni definite dall'utente che eseguono istruzioni SQL dinamiche.  
  
- L'uso della rappresentazione con la clausola EXECUTE AS Transact-SQL.  
  
- Firma di stored procedure con certificati.  
  
### <a name="execute-as"></a>EXECUTE AS  
La clausola EXECUTE AS sostituisce le autorizzazioni del chiamante con quelle dell'utente specificato nella clausola EXECUTE AS. Le stored procedure o i trigger nidificati vengono eseguiti nel contesto di sicurezza dell'utente proxy. Questo può interrompere le applicazioni che si basano sulla sicurezza a livello di riga o richiedono il controllo. Alcune funzioni che restituiscono l'identità dell'utente restituiscono l'utente specificato nella clausola EXECUTE AS, non il chiamante originale. Il contesto di esecuzione viene ripristinato al chiamante originale solo dopo l'esecuzione della procedura o quando viene eseguita un'istruzione REVERT.  
  
### <a name="certificate-signing"></a>Firma del certificato  
Quando viene eseguito un stored procedure firmato con un certificato, le autorizzazioni concesse all'utente del certificato vengono unite a quelle del chiamante. Il contesto di esecuzione rimane invariato. l'utente del certificato non rappresenta il chiamante. Per la firma di stored procedure sono necessari diversi passaggi da implementare. Ogni volta che la procedura viene modificata, è necessario firmarla nuovamente.  
  
### <a name="cross-database-access"></a>Accesso tra database  
Il concatenamento della proprietà tra database non funziona nei casi in cui vengono eseguite istruzioni SQL create dinamicamente. Per aggirare questo problema, in SQL Server è possibile creare un stored procedure che accede ai dati di un altro database e firmare la procedura con un certificato disponibile in entrambi i database. Ciò consente agli utenti di accedere alle risorse di database utilizzate dalla procedura senza concedere loro l'accesso al database o le autorizzazioni.  
  
## <a name="external-resources"></a>Risorse esterne  
Per ulteriori informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[Stored procedure](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md) e [SQL injection](../../../relational-databases/security/sql-injection.md) nella documentazione online di SQL Server|Negli argomenti viene descritto come creare stored procedure e come funziona SQL injection.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Scenari di sicurezza delle applicazioni in SQL Server](application-security-scenarios-sql-server.md)
