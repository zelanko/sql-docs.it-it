---
title: Le funzioni definite dall'utente non sono consentite nelle system_function_schema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 10813b7bc0a97f0ba8a81f3f48447142659cd596
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091326"
---
# <a name="user-defined-functions-are-not-allowed-in-system_function_schema"></a>In system_function_schema non sono consentite funzioni definite dall'utente
  Sono state rilevate funzioni definite dall'utente di proprietà dell'utente non documentato **system_function_schema**. Non è possibile creare una funzione di sistema definita dall'utente specificando tale utente. Il nome utente **system_function_schema** non esiste e l'ID utente associato a questo nome (UID = 4) è riservato allo schema **sys** ed è limitato a un uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Le operazioni di archiviazione e accesso agli oggetti di sistema sono state modificate nei modi seguenti:  
  
-   Gli oggetti di sistema sono archiviati nel database **Resource** di sola lettura e gli aggiornamenti diretti degli oggetti di sistema non sono consentiti.  
  
     Gli oggetti di sistema vengono visualizzati logicamente nello schema **sys** di ogni database. In questo modo è possibile richiamare le funzioni di sistema da qualsiasi database specificando un nome di funzione composto da una sola parte. Ad esempio, l'istruzione `SELECT * FROM fn_helpcollations()` può essere eseguita da qualsiasi database.  
  
-   Il **system_function_schema** utente non documentato è stato rimosso.  
  
-   L'ID utente associato a **system_function_schema** (UID = 4) è riservato allo schema **sys** ed è limitato a un uso interno.  
  
 Queste modifiche hanno l'effetto seguente sulle funzioni di sistema definite dall'utente:  
  
-   Le istruzioni DDL (Data Definition Language) che fanno riferimento a **system_function_schema** avranno esito negativo. Ad esempio, l'istruzione `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... avrà esito negativo.  
  
-   Dopo l'aggiornamento a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], gli oggetti esistenti di proprietà di **system_function_schema** sono contenuti solo nello schema **sys** del database **Master** . Poiché gli oggetti di sistema non possono essere modificati, queste funzioni non possono mai essere modificate o eliminate dal database **Master** . Inoltre, non possono essere richiamate da altri database specificando un nome di funzione composto da una sola parte.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di eseguire l'aggiornamento, completare le attività seguenti:  
  
1.  Modificare la proprietà delle funzioni definite dall'utente esistenti in **dbo** usando il stored procedure di sistema **sp_changeobjectowner** .  
  
2.  Rinominare la funzione in modo da non utilizzare il prefisso 'fn_' per evitare potenziali conflitti di nome con le funzioni di sistema correnti o future.  
  
3.  Aggiungere una copia delle funzioni modificate in ogni database in cui vengono utilizzate.  
  
4.  Sostituire i riferimenti a **system_function_schema** con **dbo** in tutti gli script che contengono istruzioni DDL di funzioni definite dall'utente.  
  
5.  Modificare gli script che richiamano queste funzioni per utilizzare il nome in due parti dbo **.** _function_name_o il nome in tre parti _database_name_**.** dbo. *function_name*.  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti della documentazione online di SQL Server:  
  
-   "sp_changeobjectowner"  
  
-   "Separazione fra schema e utente"  
  
-   "Database Resource"  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)   
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Rimuovere istruzioni che modificano oggetti di sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Rimuovere le istruzioni che eliminano oggetti di sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
