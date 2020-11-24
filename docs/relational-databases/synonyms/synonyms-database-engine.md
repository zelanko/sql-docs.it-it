---
description: Sinonimi (Motore di database)
title: Sinonimi (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74f5c5dcf2f2e1891daca22d70ebb9d9f1d9119f
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983115"
---
# <a name="synonyms-database-engine"></a>Sinonimi (Motore di database)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un sinonimo è un oggetto di database che viene utilizzato per gli scopi seguenti:  
  
-   Fornisce un nome alternativo per un altro oggetto di database, definito oggetto di base, presente su un server locale o remoto.  
  
-   Fornisce un livello di astrazione che consente di proteggere un'applicazione client dalle modifiche apportate al nome o alla posizione dell'oggetto di base.  
  
Si consideri ad esempio la tabella **Employee** di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], che si trova su un server denominato **Server1**. Per farvi riferimento da un altro server, **Server2**, un'applicazione client dovrebbe usare il nome composto da quattro parti **Server1.AdventureWorks.Person.Employee**. Inoltre, se la tabella venisse spostata in un altro server, sarebbe necessario modificare l'applicazione client in modo da riflettere la modifica della posizione.  
  
Per risolvere entrambi i problemi, è possibile creare un sinonimo, **EmpTable**, in **Server2** per la tabella **Employee** in **Server1**. L'applicazione client dovrà quindi usare unicamente il nome composto da una parte, **EmpTable**, per fare riferimento alla tabella **Employee** . Se la posizione della tabella **Employee** viene modificata, sarà necessario modificare il sinonimo, **EmpTable**, per puntare alla nuova posizione della tabella **Employee** . Poiché non esiste un'istruzione ALTER SYNONYM, è necessario prima eliminare il sinonimo, **EmpTable**, quindi ricrearlo con lo stesso nome, ma puntando alla nuova posizione della tabella **Employee**.  
  
Un sinonimo appartiene a uno schema e, come gli altri oggetti di uno schema, deve avere un nome univoco. È possibile creare sinonimi per gli oggetti di database seguenti:  

:::row:::
    :::column:::
        Stored procedure assembly (CLR)

        Funzione scalare assembly (CLR)

        Procedura di filtro della replica

        Funzione scalare SQL

        Funzione con valori di tabella inline SQL

        Visualizzazione
    :::column-end:::
    :::column:::
        Funzione con valori di tabella assembly (CLR)

        Funzioni di aggregazione assembly (CLR)

        Funzione con valori di tabella SQL

        Stored procedure SQL

        Tabella* (definita dall'utente)
    :::column-end:::
:::row-end:::

*Include tabelle temporanee globali e locali  
  
> [!NOTE]  
> I nomi composti da quattro parti non sono supportati per gli oggetti funzione di base.  
  
Un sinonimo non può essere l'oggetto di base di un altro sinonimo e non può fare riferimento a una funzione di aggregazione definita dall'utente.  
  
L'associazione tra un sinonimo e il relativo oggetto di base avviene unicamente in base al nome. Tutti i controlli relativi all'esistenza, al tipo e alle autorizzazioni per l'oggetto di base sono rimandati alla fase di esecuzione. L'oggetto di base può pertanto essere modificato, eliminato o eliminato e sostituito da un altro oggetto con lo stesso nome dell'oggetto di base originale. Si consideri ad esempio il sinonimo **MyContacts** che fa riferimento alla tabella **Person.Contact** di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]. Se la tabella **Contact** viene eliminata e sostituita da una vista denominata **Person.Contact**, il sinonimo **MyContacts** farà riferimento alla vista **Person.Contact** .  
  
I riferimenti a sinonimi non sono associati a schemi e pertanto è possibile eliminare un sinonimo in qualsiasi momento. Se si elimina un sinonimo, si corre tuttavia il rischio di lasciare riferimenti inesatti al sinonimo eliminato, che verranno trovati solo in fase di esecuzione.  
  
## <a name="synonyms-and-schemas"></a>Sinonimi e schemi  
Se è disponibile uno schema predefinito di cui non si è proprietari e si desidera creare un sinonimo, è necessario qualificare il nome del sinonimo con il nome dello schema di cui si è proprietari. Se ad esempio si è proprietari di uno schema **x**, ma lo schema predefinito è **y** e si usa l'istruzione CREATE SYNONYM, è necessario anteporre al nome del sinonimo lo schema **x**, anziché assegnare al sinonimo un nome composto da una parte. Per altre informazioni sulla creazione dei sinonimi, vedere [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md).  
  
## <a name="granting-permissions-on-a-synonym"></a>Concessione delle autorizzazioni per un sinonimo  
Le autorizzazioni per un sinonimo possono essere concesse unicamente dai proprietari del sinonimo, membri di **db_owner** o di **db_ddladmin** .  
  
È possibile usare `GRANT`, `DENY` e `REVOKE` per concedere, negare o revocare tutte o una qualsiasi delle autorizzazioni seguenti per un sinonimo:  

:::row:::
    :::column:::
      CONTROL

      EXECUTE

      SELECT

      UPDATE
    :::column-end:::
    :::column:::
      DELETE

      INSERT

      TAKE OWNERSHIP

      VIEW DEFINITION
    :::column-end:::
:::row-end:::

## <a name="using-synonyms"></a>Utilizzo dei sinonimi  
 In diverse istruzioni SQL e contesti di espressione è possibile utilizzare sinonimi in sostituzione dell'oggetto di base a cui viene fatto riferimento. Le colonne seguenti contengono un elenco di queste istruzioni e contesti di espressione:  

:::row:::
    :::column:::
        SELECT

        UPDATE

        EXECUTE
    :::column-end:::
    :::column:::
        INSERT

        DELETE

        Sub-SELECT
    :::column-end:::
:::row-end:::
 
 Quando si utilizzano i sinonimi nei contesti citati, l'istruzione viene eseguita sull'oggetto di base. Ad esempio, se un sinonimo fa riferimento a un oggetto di base che è una tabella e si inserisce una riga nel sinonimo, la riga verrà inserita nella tabella referenziata.  
  
> [!NOTE]  
> Non è possibile fare riferimento a un sinonimo che si trova in un server collegato.  
  
 È possibile utilizzare un sinonimo come parametro per la funzione OBJECT_ID. Tuttavia, la funzione restituisce l'ID oggetto del sinonimo, anziché l'oggetto di base.  
  
 Non è possibile fare riferimento a un sinonimo in un'istruzione DDL. Ad esempio, le istruzioni seguenti, che fanno riferimento a un sinonimo denominato `dbo.MyProduct`, generano errori:  
  
```sql  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
Le istruzioni di autorizzazione seguenti sono associate solo al sinonimo e non all'oggetto di base:  

:::row:::
    :::column:::
        GRANT

        REVOKE
    :::column-end:::
    :::column:::
        NEGA
    :::column-end:::
:::row-end:::

I sinonimi non sono associati a uno schema, pertanto non è possibile farvi riferimento con i seguenti contesti di espressione associati a schema:  

:::row:::
    :::column:::
        vincoli CHECK

        Espressioni predefinite

        Viste associate a schema
    :::column-end:::
    :::column:::
        Colonne calcolate

        Espressioni di regole

        Funzioni associate a schema
    :::column-end:::
:::row-end:::
  
Per altre informazioni sulle funzioni associate a schema, vedere [Creare funzioni definite dall'utente &#40;Motore di database&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
## <a name="getting-information-about-synonyms"></a>Recupero di informazioni sui sinonimi  
La vista del catalogo `sys.synonyms` contiene una voce per ogni sinonimo incluso in un database specifico. La vista del catalogo espone i metadati dei sinonimi, ad esempio il nome del sinonimo e il nome dell'oggetto di base. Per altre informazioni, vedere [sys.synonyms &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md).  
  
Utilizzando proprietà estese, è possibile aggiungere istruzioni o descrizioni, maschere di input e regole di formattazione come proprietà di un sinonimo. Poiché la proprietà viene archiviata nel database, tutte le applicazioni che leggono la proprietà possono valutare l'oggetto nello stesso modo. Per altre informazioni, vedere [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md).  
  
Per trovare il tipo di base dell'oggetto di base di un sinonimo, utilizzare la funzione OBJECTPROPERTYEX. Per altre informazioni, vedere [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
### <a name="examples"></a>Esempi  
Nell'esempio seguente viene restituito il tipo di base dell'oggetto di base di un sinonimo che rappresenta un oggetto locale.  
  
```sql  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
Nell'esempio seguente viene restituito il tipo di base dell'oggetto di base di un sinonimo che rappresenta un oggetto remoto in un server denominato `Server1`.  
  
```sql  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>Contenuto correlato  
 [Creare sinonimi](../../relational-databases/synonyms/create-synonyms.md)    
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)    
 [DROP SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)    
  
