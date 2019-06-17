---
title: Limitazioni delle funzionalità | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506919"
---
# <a name="feature-restrictions"></a>Limitazioni delle funzionalità

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Una fonte comune di attacchi a SQL Server è tramite applicazioni Web che accedono al database in cui vengono usate varie forme di attacchi SQL injection per estrapolare informazioni sul database.  In teoria, il codice dell'applicazione viene sviluppato in modo da non consentire SQL injection.  Tuttavia, nelle grandi codebase che includono codice legacy ed esterno, non si può mai essere sicuri di prevedere tutti i casi, quindi gli attacchi SQL injection sono una realtà da cui occorre proteggersi.  L'obiettivo delle limitazioni delle funzionalità è evitare che alcune forme di SQL injection causino la divulgazione di informazioni sul database, anche quando l'attacco SQL injection riesce.

## <a name="enabling-feature-restrictions"></a>Abilitazione delle limitazioni delle funzionalità

L'abilitazione delle limitazioni delle funzionalità avviene tramite la stored procedure `sp_add_feature_restriction` come segue:

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

È possibile limitare le funzionalità seguenti:

| Funzionalità          | Descrizione |
|------------------|-------------|
| N'ErrorMessages' | Se limitata, tutti i dati utente all'interno del messaggio di errore verranno mascherati. Vedere [Limitazione della funzionalità dei messaggi di errore](#error-messages-feature-restriction) |
| N'Waitfor'       | Se limitata, il comando restituirà immediatamente il controllo senza alcun ritardo. Vedere [Limitazione della funzionalità WAITFOR](#waitfor-feature-restriction) |

Il valore di `object_class` può essere `N'User'` oppure `N'Role'` per indicare se `object_name` è un nome utente o un nome di ruolo nel database.

L'esempio seguente consente di mascherare tutti i messaggi di errore per l'utente `MyUser`:

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>Disabilitazione delle limitazioni delle funzionalità

La disabilitazione delle limitazioni delle funzionalità avviene tramite la stored procedure `sp_drop_feature_restriction` come segue:

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

L'esempio seguente disabilita il mascheramento dei messaggi di errore per l'utente `MyUser`:

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>Visualizzazione delle limitazioni delle funzionalità

La vista `sys.sql_feature_restrictions` presenta tutte le limitazioni delle funzionalità attualmente definite nel database. Vedere [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md) per informazioni sulla modalità.

## <a name="feature-restrictions"></a>Limitazioni delle funzionalità

### <a name="error-messages-feature-restriction"></a>Limitazione della funzionalità dei messaggi di errore

Un metodo comune per un attacco SQL injection prevede l'inserimento di codice che causa un errore.  Esaminando il messaggio di errore, un utente malintenzionato può raccogliere informazioni relative al sistema, rendendo possibili ulteriori attacchi più mirati.  Questo attacco può essere particolarmente utile quando l'applicazione non visualizza i risultati di una query, ma visualizza messaggi di errore.

Si consideri un'applicazione Web con una richiesta nel formato seguente:

```html
http://www.contoso.com/employee.php?id=1
```

Che esegue la query di database seguente:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Se il valore passato come parametro `Id` alla richiesta dell'applicazione Web viene copiato per sostituire $EmpId nella query del database, un utente malintenzionato potrebbe eseguire la richiesta seguente:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

E verrebbe restituito l'errore seguente, che consente all'autore dell'attacco di ottenere il nome del database:

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

Dopo l'abilitazione della limitazione della funzionalità dei messaggi di errore per l'utente dell'applicazione nel database, il messaggio di errore restituito viene mascherato in modo che non venga divulgata alcuna informazione interna sul database:

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

Analogamente, l'autore dell'attacco potrebbe eseguire la richiesta seguente:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

E verrebbe restituito l'errore seguente, che consente all'autore dell'attacco di venire a conoscenza dello stipendio del dipendente:

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

Se si usa la limitazione della funzionalità dei messaggi di errore, il database restituisce:

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>Limitazione della funzionalità WAITFOR

Un attacco Blind SQL Injection si verifica quando un'applicazione non fornisce all'utente malintenzionato i risultati del codice SQL inserito o un messaggio di errore, ma l'autore dell'attacco può dedurre informazioni dal database mediante la costruzione di una query condizionale in cui i due rami condizionali richiedono una quantità di tempo diversa per l'esecuzione. Confrontando il tempo di risposta, l'autore dell'attacco può sapere quale ramo è stato eseguito e in tal modo raccogliere informazioni relative al sistema. La variante più semplice di questo tipo di attacco prevede l'uso dell'istruzione `WAITFOR` per introdurre il ritardo.

Si consideri un'applicazione Web con una richiesta nel formato seguente:

```html
http://www.contoso.com/employee.php?id=1
```

che esegue la query di database seguente:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Se il valore passato come parametro `Id` alle richieste dell'applicazione Web viene copiato per sostituire $EmpId nella query del database, un utente malintenzionato può eseguire la richiesta seguente:

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

E la query richiederebbe ulteriori 5 secondi se venisse usato l'account `sa`. Se la limitazione delle funzionalità `WAITFOR` è disabilitata nel database, l'istruzione `WAITFOR` verrà ignorata e non si verificheranno perdite di informazioni con questo attacco.
