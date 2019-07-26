---
title: Concedere le autorizzazioni di database per l'esecuzione di script R e Python
description: Come concedere le autorizzazioni utente del database per l'esecuzione di script R e Python in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: be6d23c6b176e8d7b2c9bf0d7ff7a02212509a10
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469835"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Concedere agli utenti le autorizzazioni per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come concedere agli utenti le autorizzazioni per l'esecuzione di script esterni in SQL Server Machine Learning Services e per concedere autorizzazioni di lettura, scrittura o Data Definition Language (DDL) ai database.

Per ulteriori informazioni, vedere la sezione autorizzazioni in [Cenni preliminari sulla sicurezza per Extensibility Framework](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Autorizzazione per l'esecuzione di script

Se si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installato manualmente e si eseguono script R o Python nella propria istanza, in genere si eseguono gli script come amministratore. In questo modo si dispone di autorizzazioni implicite per varie operazioni e per tutti i dati nel database.

La maggior parte degli utenti, tuttavia, non dispone di autorizzazioni elevate. Ad esempio, gli utenti di un'organizzazione che utilizzano account di accesso SQL per accedere al database in genere non dispongono di autorizzazioni elevate. Pertanto, per ogni utente che usa R o Python, è necessario concedere agli utenti di Machine Learning Services l'autorizzazione per eseguire script esterni in ogni database in cui viene usata la lingua. Ecco come:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Le autorizzazioni non sono specifiche del linguaggio di scripting supportato. In altre parole, non sono disponibili livelli di autorizzazione separati per script R e script Python. Se è necessario mantenere autorizzazioni separate per queste lingue, installare R e Python in istanze separate.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>GRANT-autorizzazioni per i database

Mentre un utente esegue gli script, potrebbe essere necessario che l'utente legga i dati da altri database. Potrebbe inoltre essere necessario creare nuove tabelle per archiviare i risultati e scrivere dati nelle tabelle.

Per ogni account utente di Windows o account di accesso SQL che esegue script R o Python, verificare che disponga delle autorizzazioni appropriate per il database specifico `db_datareader` : per leggere i `db_datawriter` dati, salvare oggetti nel database o `db_ddladmin` creare oggetti come le stored procedure o le tabelle contenenti dati sottoposti a training e serializzati.

Ad esempio, l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente assegna all'account di accesso SQL *MySQLLogin* i diritti per l'esecuzione di query T-SQL nel database *ML_Samples* . Per eseguire questa istruzione, l'account di accesso SQL deve essere già presente nel contesto di sicurezza del server.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle autorizzazioni incluse in ogni ruolo, vedere [ruoli a livello di database](../../relational-databases/security/authentication-access/database-level-roles.md).