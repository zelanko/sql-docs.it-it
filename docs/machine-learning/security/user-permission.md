---
title: Concedere le autorizzazioni per l'esecuzione di script Python e R
description: Informazioni su come concedere agli utenti l'autorizzazione per l'esecuzione di script Python e R esterni in Machine Learning Services per SQL Server e le autorizzazioni di lettura, scrittura o DDL (Data Definition Language) per i database.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/03/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019, contperfq4
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: da601b8c83e6e226da0329ec8d8c732d9877656a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775362"
---
# <a name="grant-users-permission-to-execute-python-and-r-scripts-with-sql-server-machine-learning-services"></a>Concedere agli utenti le autorizzazioni per l'esecuzione di script Python e R con Machine Learning Services per SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Informazioni su come concedere agli utenti l'autorizzazione per l'esecuzione di script Python e R esterni in [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) e le autorizzazioni di lettura, scrittura o DDL (Data Definition Language) per i database.

Per altre informazioni, vedere la sezione sulle autorizzazioni in [Panoramica della sicurezza per il framework di estendibilità](../../machine-learning/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Autorizzazione per l'esecuzione di script

Per ogni utente che esegue script Python o R con Machine Learning Services per SQL Server e che non è un amministratore, è necessario concedere l'autorizzazione per l'esecuzione di script esterni in ogni database in cui viene usato il linguaggio.

Per concedere l'autorizzazione per l'esecuzione di script esterni, eseguire lo script seguente:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Le autorizzazioni non sono specifiche del linguaggio di scripting supportato. In altre parole, non esistono livelli di autorizzazione separati per script R e script Python.

<a name="permissions-db"></a>

## <a name="grant-databases-permissions"></a>Concedere autorizzazioni per i database

Mentre esegue alcuni script, un utente può avere bisogno di leggere dati da altri database, nonché di creare nuove tabelle per archiviare i risultati e scrivere dati nelle tabelle.

Assicurarsi che ogni account utente Windows o ogni account di accesso SQL che esegue script R o Python abbia le autorizzazioni appropriate per il database specifico: 

+ `db_datareader` per la lettura dei dati.
+ `db_datawriter` per il salvataggio degli oggetti nel database.
+ `db_ddladmin` per la creazione di oggetti come stored procedure o tabelle contenenti dati sottoposti a training e serializzati.

L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente, ad esempio, concede all'account di accesso SQL *MySQLLogin* i diritti per l'esecuzione di query T-SQL nel database *ML_Samples*. Per eseguire questa istruzione, l'account di accesso SQL deve essere già presente nel contesto di sicurezza del server.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle autorizzazioni incluse in ogni ruolo, vedere [Ruoli a livello di database](../../relational-databases/security/authentication-access/database-level-roles.md).
