---
title: In system_function_schema non sono consentite funzioni definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b7c21521fbdd4a4e80ed196c67c72f790341f020
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254276"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>In system_function_schema non sono consentite funzioni definite dall'utente
  Rilevate funzioni definite dall'utente che sono proprietà dell'utente non documentato **system_function_schema**. Non è possibile creare una funzione di sistema definita dall'utente specificando tale utente. Il **system_function_schema** il nome utente non esiste e l'ID utente associato con questo nome (UID = 4) è riservato per il **sys** schema ed è limitato al solo uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Le operazioni di archiviazione e accesso agli oggetti di sistema sono state modificate nei modi seguenti:  
  
-   Gli oggetti di sistema vengono archiviati in sola lettura **risorsa** , del database e indirizzare gli aggiornamenti di oggetto di sistema non sono consentiti.  
  
     Gli oggetti di sistema sono visualizzate logicamente nel **sys** schema di ogni database. In questo modo è possibile richiamare le funzioni di sistema da qualsiasi database specificando un nome di funzione composto da una sola parte. Ad esempio, l'istruzione `SELECT * FROM fn_helpcollations()` può essere eseguita da qualsiasi database.  
  
-   L'utente non documentato **system_function_schema** è stata rimossa.  
  
-   L'ID utente associato **system_function_schema** (UID = 4) è riservato per il **sys** schema ed è limitato al solo uso interno.  
  
 Queste modifiche hanno l'effetto seguente sulle funzioni di sistema definite dall'utente:  
  
-   Istruzioni Data Definition Language (DDL) che fanno riferimento a **system_function_schema** avrà esito negativo. Ad esempio, l'istruzione `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... non verrà completata.  
  
-   Dopo l'aggiornamento a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], gli oggetti esistenti che sono di proprietà **system_function_schema** sono contenuti solo nel **sys** dello schema del **master** database. Poiché gli oggetti di sistema non possono essere modificati, queste funzioni mai possono essere modificate o eliminate dal **master** database. Inoltre, non possono essere richiamate da altri database specificando un nome di funzione composto da una sola parte.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di eseguire l'aggiornamento, completare le attività seguenti:  
  
1.  Modificare la proprietà delle funzioni definite dall'utente esistenti a **dbo** tramite il **sp_changeobjectowner** stored procedure di sistema.  
  
2.  Rinominare la funzione in modo da non utilizzare il prefisso 'fn_' per evitare potenziali conflitti di nome con le funzioni di sistema correnti o future.  
  
3.  Aggiungere una copia delle funzioni modificate in ogni database in cui vengono utilizzate.  
  
4.  Sostituire i riferimenti a **system_function_schema** con **dbo** in tutti gli script che contengono istruzioni DDL di funzioni definite dall'utente.  
  
5.  Modificare gli script che richiamano tali funzioni per l'utilizzo di dbo nome in due parti **.** _nome_funzione_, o il nome in tre parti _database_name_**.** dbo. *nome_funzione*.  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti della documentazione online di SQL Server:  
  
-   "sp_changeobjectowner"  
  
-   "Separazione fra schema e utente"  
  
-   "Database Resource"  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)   
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Rimuovere le istruzioni che modificano oggetti di sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Rimuovere le istruzioni che eliminano oggetti di sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
