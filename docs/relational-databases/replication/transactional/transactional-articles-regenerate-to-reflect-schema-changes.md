---
title: Rigenerare procedure personalizzate per le modifiche dello schema (transazionale)
description: Rigenerare stored procedure transazionali personalizzate per riflettere le modifiche dello schema per la replica transazionale.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 9616c11a1d17f2634ef0b525dd23ac8b31203ddc
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159389"
---
# <a name="transactional-articles---regenerate-to-reflect-schema-changes"></a>Articoli transazionali - Rigenerare per riflettere le modifiche dello schema
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  Per impostazione predefinita, la replica transazionale apporta tutte le modifiche di dati nei Sottoscrittori tramite stored procedure generate mediante procedure interne per ogni articolo di tabella nella pubblicazione. Le tre procedure, rispettivamente per inserimenti, aggiornamenti ed eliminazioni, vengono copiate nel Sottoscrittore ed eseguite in caso di replica di un inserimento, un aggiornamento o un'eliminazione nel Sottoscrittore. Quando viene apportata una modifica dello schema a una tabella in un server di pubblicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , queste procedure vengono rigenerate automaticamente dalla replica chiamando lo stesso set di procedure di scripting interne affinché le nuove procedure corrispondano al nuovo schema. La replica di modifiche dello schema non è supportata per i server di pubblicazione Oracle.  
  
 È inoltre possibile specificare procedure personalizzate per sostituire una o più procedure predefinite. Le procedure personalizzate vanno modificate in caso di modifica dello schema che influisce sulla procedura. Ad esempio, se una procedura fa riferimento a una colonna eliminata con una modifica dello schema, occorre rimuovere i riferimenti alla colonna dalla procedura. Per propagare una nuova procedura personalizzata ai Sottoscrittori con la replica sono disponibili due modi.  
  
-   La prima opzione consiste nell'utilizzare una procedura di scripting personalizzata per sostituire le impostazioni predefinite utilizzate dalla replica:  
  
    1.  Quando si esegue [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), assicurarsi che il bit 0x02 di `@schema_option` sia impostato su **true**.  
  
    2.  Eseguire [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) e specificare un valore "insert", "update" o "delete" per il parametro `@type` e il nome della procedura di scripting personalizzata per il parametro `@value`.  
  
     Alla successiva modifica dello schema, la replica chiama questa stored procedure per inserire nello script la definizione per la nuova stored procedure personalizzata definita dall'utente e quindi propaga la procedura a ogni Sottoscrittore.  
  
-   La seconda opzione consiste nell'utilizzare uno script contenente una nuova definizione di procedura personalizzata:  
  
    1.  Quando si esegue [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), impostare il bit 0x02 di `@schema_option` su **false** affinché la replica non generi automaticamente procedure personalizzate nel Sottoscrittore.  
  
    2.  Prima di ogni modifica dello schema, creare un nuovo file script e registrare lo script con la replica eseguendo [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Specificare un valore "custom_script" per il parametro `@type` e il percorso dello script nel server di pubblicazione per il parametro `@value`.  
  
     Alla successiva modifica significativa dello schema, questo script viene eseguito in ogni Sottoscrittore all'interno della stessa transazione del comando DDL. Dopo che è stata apportata la modifica dello schema, la registrazione dello script viene annullata. Per consentire l'esecuzione dello script dopo una successiva modifica dello schema, è necessario registrarlo nuovamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Apportare modifiche allo schema nei database di pubblicazione](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
