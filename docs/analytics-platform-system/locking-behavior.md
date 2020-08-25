---
title: Comportamento di blocco
description: Informazioni sul modo in cui data warehouse parallelo utilizza il blocco per garantire l'integrità delle transazioni e mantenere la coerenza dei database quando più utenti accedono contemporaneamente ai dati.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74401004"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamento di blocco in parallelo data warehouse
Informazioni sul modo in cui data warehouse parallelo utilizza il blocco per garantire l'integrità delle transazioni e mantenere la coerenza dei database quando più utenti accedono contemporaneamente ai dati.  
  
## <a name="locking-basics"></a><a name="Basics"></a>Nozioni fondamentali sui blocchi  
**Modalità**  
  
SQL Server PDW supporta quattro modalità di blocco:  
  
Esclusivo  
Il blocco esclusivo impedisce la scrittura o la lettura dall'oggetto bloccato fino al completamento della transazione che mantiene il blocco esclusivo. Non sono consentiti altri blocchi in modalità mentre è attivo il blocco esclusivo. Ad esempio, DROP TABLE e CREATE DATABASE utilizzano un blocco esclusivo.  
  
Condiviso  
Il blocco condiviso impedisce l'avvio di un blocco esclusivo sull'oggetto interessato, ma consente tutte le altre modalità di blocco. Ad esempio, l'istruzione SELECT avvia un blocco condiviso e pertanto consente a più query di accedere simultaneamente ai dati selezionati, ma impedisce gli aggiornamenti ai record letti, fino al completamento dell'istruzione SELECT.  
  
ExclusiveUpdate  
Il blocco ExclusiveUpdate impedisce la scrittura nell'oggetto bloccato, ma consente la lettura tramite il blocco condiviso. Non sono consentiti altri blocchi mentre è attivo il blocco ExclusiveUpdate. Ad esempio, BACKUP DATABASE e RESTOre DATABASE utilizzano un blocco di aggiornamento esclusivo.  
  
SharedUpdate  
Il blocco SharedUpdate impedisce le modalità di blocco Exclusive e ExclusiveUpdate e consente le modalità di blocco Shared e SharedUpdate sull'oggetto. SharedUpdate modifica un oggetto, ma non limita l'accesso in lettura a tale oggetto durante la modifica. Ad esempio, INSERT e UPDATE usano un blocco SharedUpdate.  
  
**Classi di risorse**  
  
I blocchi vengono mantenuti nelle classi di oggetti seguenti: DATABASE, SCHEMA, oggetto (tabella, vista o procedura), applicazione (utilizzata internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT e SCHEMARESOLUTION (un blocco a livello di database durante la creazione, la modifica o l'eliminazione di oggetti dello schema o di utenti del database). Queste classi di oggetti possono essere visualizzate nella colonna object_type di [sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="general-remarks"></a><a name="Remarks"></a>Osservazioni generali  
I blocchi possono essere applicati a database, tabelle o viste.  
  
SQL Server PDW non implementa alcun livello di isolamento configurabile. Supporta il livello di isolamento READ_UNCOMMITTED come definito dallo standard ANSI. Tuttavia, poiché le operazioni di lettura vengono eseguite in READ_UNCOMMITTED, pochissime operazioni di blocco si verificano o comportano una contesa nel sistema.  
  
SQL Server PDW si basa sul motore di SQL Server sottostante per implementare il blocco e il controllo della concorrenza. Se le operazioni portano a un deadlock SQL Server sottostante nello stesso nodo, SQL Server PDW sfrutta la funzionalità di rilevamento dei deadlock SQL Server e termina una delle istruzioni di blocco.  
  
> [!NOTE]  
> SQL Server non consente istruzioni in attesa che i blocchi vengano bloccati dalle richieste di blocco più recenti. Il processo non è stato completamente implementato da SQL Server PDW. In SQL Server PDW, le richieste continue per i nuovi blocchi condivisi possono a volte bloccare una richiesta precedente (ma in attesa) per un blocco esclusivo. Ad esempio, un'istruzione **Update** (che richiede un blocco esclusivo) può essere bloccata da blocchi condivisi concessi per serie di istruzioni **SELECT** . Per risolvere un processo bloccato (identificato esaminando [sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), interrompere l'invio di nuove richieste finché il blocco esclusivo non è stato soddisfatto.  
  
## <a name="lock-definition-table"></a>Tabella definizione blocco  
SQL Server supporta i tipi di blocchi seguenti. Non tutti i tipi di blocco sono disponibili nel nodo di controllo, ma possono verificarsi nei nodi di calcolo.  
  
-   SCH-S (stabilità dello schema). Impedisce che un elemento dello schema, ad esempio una tabella o un indice, venga eliminato mentre in una sessione viene mantenuto attivo un blocco di stabilità dello schema su tale elemento.  
  
-   SCH-M (modifica dello schema). Deve essere impostato in tutte le sessioni in cui si desidera modificare lo schema della risorsa specificata. Assicura che nessun'altra sessione faccia riferimento all'oggetto specificato.  
  
-   S (condiviso). La sessione attiva dispone dell'accesso condiviso alla risorsa.  
  
-   U (aggiornamento). Indica un blocco di aggiornamento acquisito su risorse che potrebbero essere aggiornate. Viene utilizzato per evitare una forma comune di deadlock che si verifica quando in più sessioni vengono bloccate risorse che potrebbero essere aggiornate in futuro.  
  
-   X (esclusivo). La sessione attiva dispone dell'accesso esclusivo alla risorsa.  
  
-   IS (preventivo condiviso). Indica l'intenzione di impostare blocchi condivisi (S) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   IU (preventivo aggiornamento). Indica l'intenzione di impostare blocchi di aggiornamento (U) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   IX (preventivo esclusivo). Indica l'intenzione di impostare blocchi esclusivi (X) su alcune risorse subordinate nella gerarchia dei blocchi.  
  
-   SIU (Shared Intent Update). Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi di aggiornamento su risorse subordinate nella gerarchia dei blocchi.  
  
-   SIX (condiviso preventivo esclusivo). Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.  
  
-   UIX (aggiornamento preventivo esclusivo). Indica un blocco di aggiornamento attivato su una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.  
  
-   Bu. Utilizzato dalle operazioni bulk.  
  
-   RangeS_S (blocco condiviso intervalli di chiavi e risorse condivise). Indica un'analisi di intervallo serializzabile.  
  
-   RangeS_U (blocco condiviso intervallo di chiavi e aggiornamento risorsa). Indica un'analisi di aggiornamento serializzabile.  
  
-   RangeI_N (Inserisci blocco di intervalli di chiavi e risorsa null). Utilizzato per verificare gli intervalli prima di inserire una nuova chiave in un indice.  
  
-   RangeI_S. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e S.  
  
-   RangeI_U. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e U.  
  
-   RangeI_X. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e X.  
  
-   RangeX_S. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e RangeS_S.  
  
-   RangeX_U. Blocco conversione intervalli di chiavi, creato da una sovrapposizione di blocchi RangeI_N e RangeS_U.  
  
-   RangeX_X (blocco esclusivo intervalli di chiavi e risorse). Si tratta di un blocco di conversione utilizzato quando viene aggiornata una chiave in un intervallo.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
