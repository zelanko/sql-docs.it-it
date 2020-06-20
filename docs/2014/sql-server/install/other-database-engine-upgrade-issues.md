---
title: Altri problemi di aggiornamento motore di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2890a61850526f7506713b3f900d67b8d41d0bfb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012142"
---
# <a name="other-database-engine-upgrade-issues"></a>Altri problemi di aggiornamento del motore di database
  I problemi di aggiornamento seguenti non possono essere rilevati dalla versione corrente di Preparazione aggiornamento. Esaminare i problemi elencati di seguito per valutarne il potenziale impatto sui sistemi.  
  
## <a name="multiple-database-engine-deprecated-features"></a>Più caratteristiche deprecate del motore di database  
 Le opzioni o le istruzioni di [!INCLUDE[tsql](../../includes/tsql-md.md)] riportate di seguito sono deprecate:  
  
-   Opzioni NO_LOG e TRUNCATE_ONLY di BACKUP LOG  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 Utilizzo del protocollo VIA per connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] è deprecato.  
  
## <a name="new-data-types"></a>Nuovi tipi di dati  
 I seguenti tipi di dati sono tipi di sistema riservati. Rinominare i tipi definiti dall'utente (UDT) in conflitto prima o dopo l'aggiornamento.  
  
-   Area geografica  
  
-   Geometry  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>La tabella di destinazione della clausola OUTPUT INTO non può contenere trigger definiti  
 L'OUTPUT in una tabella di destinazione quando la tabella contiene trigger abilitati non è supportato.  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>Errore in fase di compilazione per le funzioni definite dall'utente quando la destinazione di una clausola OUTPUT INTO è una tabella  
 Non è possibile utilizzare funzioni definite dall'utente per eseguire azioni che modificano lo stato del database. Ad esempio, una funzione definita dall'utente non può eseguire azioni DDL (CREATE/ALTER/DROP) o DML (INSERT/UPDATE/DELETE) su qualsiasi oggetto, ad eccezione delle variabili di tabella.  
  
## <a name="merge-is-a-reserved-keyword"></a>MERGE è una parola chiave riservata  
 MERGE è ora una parola chiave completamente riservata. Non è più possibile includere oggetti (tabella, colonna e così via) denominati MERGE nelle applicazioni.  
  
## <a name="rename-cdc-schema"></a>Rinominare lo schema CDC  
 È disponibile un nome di schema denominato CDC Il nome dello schema non può essere utilizzato se **Change Data Capture** è abilitato per il database.  
  
 Prima di abilitare **Change Data Capture** per il database, è necessario eliminare lo schema cdc. Questo passaggio può essere completato prima o dopo l'aggiornamento. Per eliminare lo schema, eseguire le operazioni seguenti:  
  
1.  Trasferire gli oggetti dallo schema CDC in un nuovo schema utilizzando ALTER SCHEMA.  
  
2.  Verificare le autorizzazioni per gli oggetti nel nuovo schema.  
  
3.  Apportare le modifiche necessarie all'applicazione.  
  
4.  Eliminare lo schema CDC utilizzando DROP SCHEMA.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
