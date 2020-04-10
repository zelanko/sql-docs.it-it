---
title: Scenari di sicurezza delle applicazioni in SQL Server
description: Sono contenuti argomenti che illustrano diversi scenari di sicurezza per applicazioni ADO.NET e SQL Server.
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e686e404ab4c948811b217291d1a9a7d2adc9feb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928954"
---
# <a name="application-security-scenarios-in-sql-server"></a>Scenari di sicurezza delle applicazioni in SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Non esiste un unico modo corretto per creare un'applicazione client SQL Server sicura. Ogni applicazione è unica per requisiti, ambiente di distribuzione e popolazione di utenti. Un'applicazione ragionevolmente sicura quando viene distribuita inizialmente può diventare meno sicura nel corso del tempo. Non è possibile prevedere con precisione le minacce che potrebbero emergere in futuro.  
  
SQL Server, come prodotto, si è evoluto versione dopo versione per incorporare le funzionalità di sicurezza più recenti che consentono agli sviluppatori di creare applicazioni di database sicure. Tuttavia, la sicurezza non è un prodotto preconfezionato, richiede monitoraggio e aggiornamento continui.  
  
## <a name="common-threats"></a>Minacce comuni  
Gli sviluppatori devono comprendere le minacce per la sicurezza, gli strumenti disponibili per contrastarle e come evitare di creare loro stessi problemi di sicurezza. La sicurezza può essere considerata come una catena, in cui la rottura di un solo elemento compromette la forza dell'intero sistema. Nell'elenco seguente sono incluse alcune minacce di sicurezza comuni che vengono discusse più dettagliatamente negli argomenti in questa sezione.  
  
### <a name="sql-injection"></a>attacco intrusivo nel codice SQL  
L'attacco SQL injection è il processo con cui un utente malintenzionato immette istruzioni Transact-SQL anziché un input valido. Se l'input viene passato direttamente al server senza essere convalidato e se l'applicazione esegue inavvertitamente il codice inserito, è possibile che l'attacco danneggi o distrugga i dati. Per contrastare gli attacchi SQL injection è possibile usare stored procedure e comandi con parametri, evitando SQL dinamico e limitando le autorizzazioni per tutti gli utenti.  
  
### <a name="elevation-of-privilege"></a>Elevazione dei privilegi  
Gli attacchi di elevazione dei privilegi si verificano quando un utente può assumere i privilegi di un account attendibile, ad esempio un proprietario o un amministratore. Usare sempre account utente con privilegi minimi e assegnare solo le autorizzazioni necessarie. Evitare di usare account amministrativi o proprietari per l'esecuzione del codice. Questo limita la quantità di danni che possono verificarsi in caso di esito positivo di un attacco. Quando si eseguono attività che richiedono autorizzazioni aggiuntive, usare la firma delle stored procedure o la rappresentazione solo per la durata dell'attività. È possibile firmare le stored procedure con certificati o usare la rappresentazione per assegnare autorizzazioni temporanee.  
  
### <a name="probing-and-intelligent-observation"></a>Probing e osservazione intelligente  
Un attacco di tipo probing può usare i messaggi di errore generati da un'applicazione per cercare vulnerabilità di sicurezza. Implementare la gestione degli errori in tutto il codice procedurale per evitare che le informazioni sugli errori SQL Server vengano restituite all'utente finale.  
  
### <a name="authentication"></a>Authentication  
Quando si usano account di accesso di SQL Server può verificarsi un attacco injection alla stringa di connessione se una stringa di connessione basata sull'input dell'utente viene costruita in fase di esecuzione. Se non viene verificata la presenza di coppie di parole chiave valide per la stringa di connessione, un utente malintenzionato può inserire caratteri aggiuntivi, accedendo potenzialmente a dati sensibili o ad altre risorse nel server. Se possibile, usare l'autenticazione di Windows. Se è necessario usare account di accesso di SQL Server, usare <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> per creare e convalidare le stringhe di connessione in fase di esecuzione.  
  
### <a name="passwords"></a>Password  
Molti attacchi hanno esito positivo perché un intruso è riuscito a ottenere o indovinare la password di un utente con privilegi. Le password rappresentano la prima linea di difesa contro eventuali intrusi, pertanto l'impostazione di password complesse costituisce una misura di sicurezza fondamentale per la sicurezza del sistema. Creare e applicare criteri password per l'autenticazione in modalità mista.  
  
Assegnare sempre una password complessa all'account `sa`, anche quando si usa l'autenticazione di Windows.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Scrittura di istruzioni SQL dinamiche protette in SQL Server](writing-secure-dynamic-sql.md)  
Vengono descritte le tecniche per la scrittura di istruzioni SQL dinamiche protette usando le stored procedure.  

## <a name="next-steps"></a>Passaggi successivi
- [Sicurezza di SQL Server](sql-server-security.md)
