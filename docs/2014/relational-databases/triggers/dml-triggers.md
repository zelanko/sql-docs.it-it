---
title: Trigger DML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df06fb9ccbf4f3683877605e321207f0ca6d997e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196509"
---
# <a name="dml-triggers"></a>Trigger DML
  Un trigger DML è un tipo speciale di stored procedure che diventa effettiva automaticamente quando viene eseguito un evento del linguaggio DML (Data Manipulation Language) che influisce sulla vista o tabella definita nel trigger. Gli eventi DML includono istruzioni INSERT, UPDATE o DELETE. I trigger DML possono essere utilizzati per applicare regole business e l'integrità dei dati, eseguire query su altre tabelle e includere istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] complesse. Il trigger e l'istruzione che lo attiva vengono considerati come una singola transazione, di cui è possibile eseguire il rollback dal trigger stesso. Se viene rilevato un errore grave, ad esempio un'insufficienza di spazio su disco, viene eseguito automaticamente il rollback dell'intera transazione.  
  
## <a name="dml-trigger-benefits"></a>Vantaggi del trigger DML  
 I trigger DML sono simili ai vincoli in quanto sono in grado di applicare l'integrità di entità o di dominio. L'integrità di entità dovrebbe essere sempre applicata al livello più basso utilizzando indici che fanno parte dei vincoli PRIMARY KEY e UNIQUE oppure creati indipendentemente dai vincoli. Per applicare l'integrità di dominio è consigliabile utilizzare i vincoli CHECK, mentre per applicare l'integrità referenziale (RI) è consigliabile utilizzare i vincoli FOREIGN KEY. I trigger DML sono particolarmente utili quando le caratteristiche supportate dai vincoli non sono in grado di soddisfare le esigenze funzionali dell'applicazione.  
  
 Nell'elenco seguente i trigger DML vengono confrontati con i vincoli e vengono identificati i casi in cui i trigger DML presentano vantaggi rispetto ai vincoli.  
  
-   I trigger DML consentono di propagare le modifiche nelle tabelle correlate del database, tuttavia è possibile eseguire le modifiche in modo più efficiente utilizzando vincoli di integrità referenziale di propagazione. I vincoli FOREIGN KEY consentono di convalidare un valore di colonna soltanto se corrisponde esattamente al valore di un'altra colonna, a meno che la clausola REFERENCES non definisca un'operazione referenziale di propagazione.  
  
-   Assicurano la protezione contro operazioni INSERT, UPDATE e DELETE dannose o non corrette e applicano altre restrizioni più complesse rispetto a quelle definite con i vincoli CHECK.  
  
     A differenza dei vincoli CHECK, i trigger DML possono fare riferimento alle colonne di altre tabelle. Un trigger, ad esempio, può utilizzare un'istruzione SELECT di un'altra tabella per eseguire il confronto con i dati inseriti o aggiornati e per eseguire ulteriori operazioni, ad esempio la modifica di dati o la visualizzazione di un messaggio di errore definito dall'utente.  
  
-   Consentono di valutare lo stato di una tabella prima e dopo la modifica dei dati e di eseguire le operazioni appropriate sulla base delle differenze.  
  
-   Più trigger DML dello stesso tipo (INSERT, UPDATE o DELETE) in una tabella consentono di eseguire più operazioni diverse in risposta alla stessa istruzione di modifica.  
  
-   I vincoli sono in grado di segnalare errori soltanto tramite messaggi di errore standard di sistema. Se nell'applicazione è necessario o consigliabile utilizzare messaggi personalizzati e gestire gli errori in modo più complesso, è necessario utilizzare un trigger.  
  
-   I trigger DML impediscono di apportare modifiche che violano l'integrità referenziale o consentono di eseguirne il rollback, annullando in tal modo il tentativo di modifica dei dati. Un trigger di questo tipo potrebbe essere attivato quando si modifica una chiave esterna e il nuovo valore non corrisponde alla chiave primaria. A questo scopo tuttavia vengono normalmente utilizzati i vincoli FOREIGN KEY.  
  
-   Gli eventuali vincoli inclusi nella tabella di trigger vengono verificati dopo l'esecuzione del trigger INSTEAD OF e prima dell'esecuzione del trigger AFTER. In caso di violazione dei vincoli, viene eseguito il rollback delle azioni del trigger INSTEAD OF e il trigger AFTER non viene eseguito.  
  
## <a name="types-of-dml-triggers"></a>Tipi di trigger DML  
 Trigger AFTER  
 I trigger AFTER vengono eseguiti dopo l'esecuzione dell'azione associata all'istruzione INSERT, UPDATE, MERGE o DELETE. I trigger AFTER non vengono mai eseguiti sei si verifica una violazione di un vincolo, pertanto non possono essere utilizzati per elaborazioni che potrebbero impedire violazioni dei vincoli. Per ogni istruzione INSERT, UPDATE o DELETE specificata in un'istruzione MERGE, viene generato il trigger corrispondente per ogni operazione DML.  
  
 Trigger INSTEAD OF  
 I trigger INSTEAD OF sostituiscono le azioni standard dell'istruzione di trigger. È pertanto possibile definire un trigger per eseguire il controllo degli errori o dei valori in una o più colonne e quindi eseguire ulteriori azioni prima di inserire, aggiornare o eliminare la riga o le righe. Quando, ad esempio, quando il valore aggiornato in una colonna relativa alla paga oraria in una tabella degli stipendi supera un valore specificato, è possibile definire un trigger per generare un messaggio di errore ed eseguire il rollback della transazione oppure inserire un nuovo record in un itinerario di controllo prima di inserire il record nella tabella degli stipendi. Il vantaggio principale dei trigger INSTEAD OF consiste nel fatto che consentono alle viste non aggiornabili di supportare gli aggiornamenti. Una vista basata su più tabelle di base, ad esempio, deve utilizzare un trigger INSTEAD OF per supportare inserimenti, aggiornamenti ed eliminazioni che fanno riferimento a dati inclusi in più tabelle. Un altro vantaggio dei trigger INSTEAD OF è rappresentato dal fatto che consentono di scrivere il codice in modo da rifiutare parti di un batch accettandone altre.  
  
 Nella tabella seguente è riportato un confronto tra le funzionalità dei trigger AFTER e INSTEAD OF.  
  
|Funzione|Trigger AFTER|Trigger INSTEAD OF|  
|--------------|-------------------|------------------------|  
|Applicabilità|Tabelle|Tabelle e viste|  
|Quantità per tabella o vista|Multiplo per azione di trigger (UPDATE, DELETE e INSERT)|Singolo per azione di trigger (UPDATE, DELETE e INSERT)|  
|Riferimenti di propagazione|Nessuna restrizione|I trigger INSTEAD OF UPDATE e DELETE non sono consentiti in tabelle che rappresentano le destinazioni di vincoli di integrità per operazioni referenziali di propagazione|  
|Esecuzione|Dopo:<br /><br /> Elaborazione dei vincoli<br />Operazioni referenziali dichiarative<br />Creazione di tabelle**inserted** e **deleted**<br />Operazione di trigger|Prima: elaborazione dei vincoli<br /><br /> Invece di: operazione di trigger<br /><br /> Dopo: creazione di tabelle  **inserted** e **deleted**|  
|Ordine di esecuzione|È possibile specificare la prima e l'ultima esecuzione|Non applicabile|  
|`varchar(max)`riferimenti `nvarchar(max)`alle colonne `varbinary(max)` , e nelle tabelle **inserted** e **Deleted**|Consentito|Consentito|  
|`text`riferimenti `ntext`alle colonne `image` , e nelle tabelle **inserted** e **Deleted**|Non consentito|Consentito|  
  
 Trigger CLR  
 I trigger CLR includono i trigger AFTER e INSTEAD OF. Un trigger CLR può essere anche un trigger DDL. Anziché eseguire una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] , un trigger CLR consente di eseguire uno o più metodi scritti in codice gestito che sono membri di un assembly creato in .NET Framework e caricato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Argomento|  
|----------|-----------|  
|Viene illustrato come creare un trigger DML.|[Creare trigger DML](create-dml-triggers.md)|  
|Viene illustrato come creare un trigger CLR.|[Creare trigger CLR](create-clr-triggers.md)|  
|Viene descritto come creare un trigger DML per la gestione delle modifiche sia della singola riga che di più righe.|[Creare trigger DML per gestire più righe di dati](create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|Viene descritto come annidare trigger.|[Creare trigger annidati](create-nested-triggers.md)|  
|Viene descritto come specificare l'ordine in cui vengono generati trigger AFTER.|[Specificare i primi e gli ultimi trigger](specify-first-and-last-triggers.md)|  
|Viene descritto come utilizzare le tabelle speciali inserted e deleted nel codice del trigger.|[Usare le tabelle inserite ed eliminate](use-the-inserted-and-deleted-tables.md)|  
|Viene descritto come modificare o rinominare un trigger DML.|[Modificare o rinominare trigger DML](modify-or-rename-dml-triggers.md)|  
|Viene descritto come visualizzare informazioni sui trigger DML.|[Recuperare informazioni sui trigger DML](get-information-about-dml-triggers.md)|  
|Vengono descritte le modalità di creazione, modifica e disabilitazione dei trigger DML.|[Eliminare e disabilitare trigger DML](delete-or-disable-dml-triggers.md)|  
|Viene descritto come gestire la sicurezza dei trigger.|[Gestire la sicurezza dei trigger](manage-trigger-security.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [Funzioni del trigger &#40;Transact-SQL&#41;](/sql/t-sql/functions/trigger-functions-transact-sql)  
  
  
