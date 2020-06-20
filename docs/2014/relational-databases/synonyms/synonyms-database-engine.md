---
title: Sinonimi (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3494f4f5b13c422efb8e2a39597e131c10d81ed1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047223"
---
# <a name="synonyms-database-engine"></a>Sinonimi (Motore di database)
  Un sinonimo è un oggetto di database che viene utilizzato per gli scopi seguenti:  
  
-   Fornisce un nome alternativo per un altro oggetto di database, definito oggetto di base, presente su un server locale o remoto.  
  
-   Fornisce un livello di astrazione che consente di proteggere un'applicazione client dalle modifiche apportate al nome o alla posizione dell'oggetto di base.  
  
 Si consideri ad esempio la tabella **Employee** di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], che si trova su un server denominato **Server1**. Per farvi riferimento da un altro server, **Server2**, un'applicazione client dovrebbe usare il nome composto da quattro parti **Server1.AdventureWorks.Person.Employee**. Inoltre, se la tabella venisse spostata in un altro server, sarebbe necessario modificare l'applicazione client in modo da riflettere la modifica della posizione.  
  
 Per risolvere entrambi i problemi, è possibile creare un sinonimo, **EmpTable**, in **Server2** per la tabella **Employee** in **Server1**. L'applicazione client dovrà quindi usare unicamente il nome composto da una parte, **EmpTable**, per fare riferimento alla tabella **Employee** . Se la posizione della tabella **Employee** viene modificata, sarà necessario modificare il sinonimo, **EmpTable**, per puntare alla nuova posizione della tabella **Employee** . Poiché non esiste un'istruzione ALTER SYNONYM, è necessario prima eliminare il sinonimo, **EmpTable**, quindi ricrearlo con lo stesso nome, ma puntando alla nuova posizione della tabella **Employee**.  
  
 Un sinonimo appartiene a uno schema e, come gli altri oggetti di uno schema, deve avere un nome univoco. È possibile creare sinonimi per gli oggetti di database seguenti:  
  
|||  
|-|-|  
|Stored procedure assembly (CLR)|Funzione con valori di tabella assembly (CLR)|  
|Funzione scalare assembly (CLR)|Funzioni di aggregazione assembly (CLR)|  
|Procedura di filtro della replica|Stored procedure estesa|  
|Funzione scalare SQL|Funzione con valori di tabella SQL|  
|Funzione con valori di tabella inline SQL|Stored procedure SQL|  
|Visualizza|Tabella<sup>1</sup> (definita dall'utente)|  
  
 <sup>1</sup> include tabelle temporanee locali e globali  
  
> [!NOTE]  
>  I nomi composti da quattro parti non sono supportati per gli oggetti funzione di base.  
  
 Un sinonimo non può essere l'oggetto di base di un altro sinonimo e non può fare riferimento a una funzione di aggregazione definita dall'utente.  
  
 L'associazione tra un sinonimo e il relativo oggetto di base avviene unicamente in base al nome. Tutti i controlli relativi all'esistenza, al tipo e alle autorizzazioni per l'oggetto di base sono rimandati alla fase di esecuzione. L'oggetto di base può pertanto essere modificato, eliminato o eliminato e sostituito da un altro oggetto con lo stesso nome dell'oggetto di base originale. Si consideri ad esempio il sinonimo **MyContacts**che fa riferimento alla tabella **Person.Contact** di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]. Se la tabella **Contact** viene eliminata e sostituita da una vista denominata **Person.Contact**, il sinonimo **MyContacts** farà riferimento alla vista **Person.Contact** .  
  
 I riferimenti a sinonimi non sono associati a schemi e pertanto è possibile eliminare un sinonimo in qualsiasi momento. Se si elimina un sinonimo, si corre tuttavia il rischio di lasciare riferimenti inesatti al sinonimo eliminato, che verranno trovati solo in fase di esecuzione.  
  
## <a name="synonyms-and-schemas"></a>Sinonimi e schemi  
 Se è disponibile uno schema predefinito di cui non si è proprietari e si desidera creare un sinonimo, è necessario qualificare il nome del sinonimo con il nome dello schema di cui si è proprietari. Se ad esempio si è proprietari di uno schema **x**, ma lo schema predefinito è **y** e si usa l'istruzione CREATE SYNONYM, è necessario anteporre al nome del sinonimo lo schema **x**, anziché assegnare al sinonimo un nome composto da una parte. Per altre informazioni sulla creazione dei sinonimi, vedere [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql).  
  
## <a name="granting-permissions-on-a-synonym"></a>Concessione delle autorizzazioni per un sinonimo  
 Le autorizzazioni per un sinonimo possono essere concesse unicamente dai proprietari del sinonimo, membri di **db_owner**o di **db_ddladmin** .  
  
 È possibile concedere, negare o revocare le autorizzazioni seguenti per un sinonimo:  
  
|||  
|-|-|  
|CONTROL|Elimina|  
|EXECUTE|INSERT|  
|SELECT|TAKE OWNERSHIP|  
|UPDATE|VIEW DEFINITION|  
  
## <a name="using-synonyms"></a>Utilizzo dei sinonimi  
 In diverse istruzioni SQL e contesti di espressione è possibile utilizzare sinonimi in sostituzione dell'oggetto di base a cui viene fatto riferimento. Nella tabella seguente è riportato un elenco di tali istruzioni e contesti di espressione:  
  
|||  
|-|-|  
|SELECT|INSERT|  
|UPDATE|Elimina|  
|EXECUTE|Sub-SELECT|  
  
 Quando si utilizzano i sinonimi nei contesti citati, l'istruzione viene eseguita sull'oggetto di base. Ad esempio, se un sinonimo fa riferimento a un oggetto di base che è una tabella e si inserisce una riga nel sinonimo, la riga verrà inserita nella tabella referenziata.  
  
> [!NOTE]  
>  Non è possibile fare riferimento a un sinonimo che si trova in un server collegato.  
  
 È possibile utilizzare un sinonimo come parametro per la funzione OBJECT_ID. Tuttavia, la funzione restituisce l'ID oggetto del sinonimo, anziché l'oggetto di base.  
  
 Non è possibile fare riferimento a un sinonimo in un'istruzione DDL. Ad esempio, le istruzioni seguenti, che fanno riferimento a un sinonimo denominato `dbo.MyProduct`, generano errori:  
  
```  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
 Le istruzioni di autorizzazione seguenti sono associate solo al sinonimo e non all'oggetto di base:  
  
|||  
|-|-|  
|GRANT|NEGA|  
|REVOKE||  
  
 I sinonimi non sono associati a uno schema, pertanto non è possibile farvi riferimento con i seguenti contesti di espressione associati a schema:  
  
|||  
|-|-|  
|vincoli CHECK|Colonne calcolate|  
|Espressioni predefinite|Espressioni di regole|  
|Viste associate a schema|Funzioni associate a schema|  
  
 Per altre informazioni sulle funzioni associate a schema, vedere [Creare funzioni definite dall'utente &#40;Motore di database&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md).  
  
## <a name="getting-information-about-synonyms"></a>Recupero di informazioni sui sinonimi  
 La vista del catalogo sys.synonyms contiene una voce per ogni sinonimo incluso in un database specifico. La vista del catalogo espone i metadati dei sinonimi, ad esempio il nome del sinonimo e il nome dell'oggetto di base. Per ulteriori informazioni sulla `sys.synonyms` vista del catalogo, vedere [sys. sinonims &#40;&#41;Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-synonyms-transact-sql).  
  
 Utilizzando proprietà estese, è possibile aggiungere istruzioni o descrizioni, maschere di input e regole di formattazione come proprietà di un sinonimo. Poiché la proprietà viene archiviata nel database, tutte le applicazioni che leggono la proprietà possono valutare l'oggetto nello stesso modo. Per altre informazioni, vedere [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql).  
  
 Per trovare il tipo di base dell'oggetto di base di un sinonimo, utilizzare la funzione OBJECTPROPERTYEX. Per altre informazioni, vedere [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql).  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il tipo di base dell'oggetto di base di un sinonimo che rappresenta un oggetto locale.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
 Nell'esempio seguente viene restituito il tipo di base dell'oggetto di base di un sinonimo che rappresenta un oggetto remoto in un server denominato `Server1`.  
  
```  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>Contenuto correlato  
 [Creare sinonimi](create-synonyms.md)  
  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
  
 [DROP SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-synonym-transact-sql)  
  
  
