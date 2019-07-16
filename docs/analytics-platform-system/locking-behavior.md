---
title: Comportamento di blocco - Parallel Data Warehouse | Microsoft Docs
description: Informazioni su come Parallel Data Warehouse Usa il blocco per garantire l'integrità delle transazioni e mantenere la coerenza dei database quando più utenti accedono ai dati nello stesso momento.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d93743c83d6315e6ab9484445f344b06f80be845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960649"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamento di blocco in Parallel Data Warehouse
Informazioni su come Parallel Data Warehouse Usa il blocco per garantire l'integrità delle transazioni e mantenere la coerenza dei database quando più utenti accedono ai dati nello stesso momento.  
  
## <a name="Basics"></a>Nozioni fondamentali di blocchi  
**Modalità**  
  
SQL Server PDW supporta quattro modalità di blocco:  
  
Exclusive  
Il blocco esclusivo impedisce la scrittura o lettura dall'oggetto bloccato finché la transazione che contiene che il blocco esclusivo viene completata. Nessun altri blocchi di qualsiasi modalità sono consentite mentre è attivo il blocco esclusivo. DROP TABLE e CREATE DATABASE, ad esempio, usare un blocco esclusivo.  
  
Condivisa  
Il blocco condiviso impedisce l'avvio di un blocco esclusivo sull'oggetto interessato, ma consente a tutte le altre modalità di blocco. Ad esempio, l'istruzione SELECT avvia un blocco condiviso e pertanto consente di accedere ai dati selezionati contemporaneamente più query, ma impedisce gli aggiornamenti per i record da leggere, fino al completamento dell'istruzione SELECT.  
  
ExclusiveUpdate  
Il blocco ExclusiveUpdate impedisce la scrittura dell'oggetto bloccato, ma consente la lettura tramite il blocco condiviso. Altri blocchi non sono consentite mentre il blocco ExclusiveUpdate è attiva. DATABASE di BACKUP e ripristino nel DATABASE, ad esempio, usare un blocco di aggiornamento esclusivo.  
  
SharedUpdate  
Il blocco SharedUpdate impedisce la modalità di blocco esclusivo ed ExclusiveUpdate e consente di modalità di blocco SharedUpdate e condiviso sull'oggetto. SharedUpdate modifica un oggetto, ma non limita l'accesso in lettura a esso durante la modifica. Ad esempio, INSERT e UPDATE usare un blocco SharedUpdate.  
  
**Classi di risorse**  
  
I blocchi vengono mantenuti per le classi di oggetti seguenti: DATABASE, SCHEMA, oggetto (una tabella, vista o procedure), dell'applicazione (usata internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT e SCHEMARESOLUTION (un blocco del database a livello eseguito durante la creazione, modifica o eliminazione di oggetti dello schema o gli utenti di database). Queste classi di oggetti visualizzabili nella colonna della object_type [DM pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Osservazioni generali  
I blocchi è applicabile al database, tabelle o viste.  
  
SQL Server PDW può neimplementuje metodu eventuali livelli di isolamento può essere configurato. Supporta il livello di isolamento READ_UNCOMMITTED come definito da standard ANSI. Tuttavia, poiché le operazioni vengono eseguite con READ_UNCOMMITTED lettura, pochissime operazioni di blocco effettivamente si verificano o provocare contesa nel sistema.  
  
SQL Server PDW si basa sul motore di SQL Server sottostante per implementare il controllo di blocco e concorrenza. Se le operazioni di causare un deadlock di SQL Server sottostante all'interno dello stesso nodo, SQL Server PDW sfrutta la funzionalità di rilevamento di deadlock di SQL Server e consente di terminare una delle istruzioni di blocco.  
  
> [!NOTE]  
> SQL Server non supporta le istruzioni che sono in attesa dei blocchi vengano bloccate da richieste di blocco più recente. SQL Server PDW non completamente implementato questo processo. In SQL Server PDW, le richieste continue per i blocchi condivisi nuovi possono a volte bloccare una richiesta precedente, ma in attesa, di un blocco esclusivo. Ad esempio, un' **UPDATE** istruzione (che richiede un blocco esclusivo) può essere bloccata da blocchi condivisi che vengono concesse per la serie di **seleziona** istruzioni. Per risolvere un processo bloccato (identificate la [DM pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), interrompere l'invio di nuove richieste finché il blocco esclusivo è stata soddisfatta.  
  
## <a name="lock-definition-table"></a>Tabella di definizioni di blocco  
SQL Server supporta i seguenti tipi di blocchi. Non tutti i tipi di blocco sono disponibili nel nodo di controllo, ma possono verificarsi nei nodi di calcolo.  
  
-   Sch-S (stabilità Schema). Impedisce che un elemento dello schema, ad esempio una tabella o un indice, venga eliminato mentre in una sessione viene mantenuto attivo un blocco di stabilità dello schema su tale elemento.  
  
-   Blocco SCH-M (modifica dello Schema). Deve essere impostato in tutte le sessioni in cui si desidera modificare lo schema della risorsa specificata. Assicura che nessun'altra sessione faccia riferimento all'oggetto specificato.  
  
-   S (condiviso). La sessione attiva dispone dell'accesso condiviso alla risorsa.  
  
-   U (aggiornamento). Indica un blocco di aggiornamento acquisito su risorse che potrebbero essere aggiornate. Viene utilizzato per evitare una forma comune di deadlock che si verifica quando in più sessioni vengono bloccate risorse che potrebbero essere aggiornate in futuro.  
  
-   X (esclusivo). La sessione attiva dispone dell'accesso esclusivo alla risorsa.  
  
-   IS (preventivo condiviso). Indica l'intenzione di impostare blocchi condivisi (S) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   IU (preventivo aggiornamento). Indica l'intenzione di impostare blocchi di aggiornamento (U) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   IX (preventivo esclusivo). Indica l'intenzione di impostare blocchi esclusivi (X) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   SIU (condiviso preventivo aggiornamento). Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi di aggiornamento su risorse subordinate nella gerarchia dei blocchi.  
  
-   SEI (condiviso preventivo esclusivo). Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.  
  
-   UIX (aggiornamento preventivo esclusivo). Indica un blocco di aggiornamento attivato su una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.  
  
-   BU. Utilizzato dalle operazioni bulk.  
  
-   RangeS_S (blocco condiviso intervalli di chiavi e risorsa). Indica un'analisi di intervallo serializzabile.  
  
-   RangeS_U (blocco condiviso intervalli di chiavi e aggiornamento risorsa). Indica un'analisi di aggiornamento serializzabile.  
  
-   RangeI_N (blocco inserimento intervalli di chiavi e risorsa Null). Utilizzato per verificare gli intervalli prima di inserire una nuova chiave in un indice.  
  
-   RangeI_S. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e S.  
  
-   RangeI_U. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e U.  
  
-   RangeI_X. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e X.  
  
-   RangeX_S. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e RangeS_S.  
  
-   RangeX_U. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e RangeS_U.  
  
-   RangeX_X (blocco esclusivo intervalli di chiavi e risorsa esclusivo). Si tratta di un blocco di conversione utilizzato quando viene aggiornata una chiave in un intervallo.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
