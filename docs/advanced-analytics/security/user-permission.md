---
title: Concedere autorizzazioni per gli script
description: Come concedere autorizzazioni utente per il database per l'esecuzione di script R e Python in Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b8d3ea5c52c5c18f09097322fdc1e1b2321494e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727303"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Concedere agli utenti l'autorizzazione per Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come concedere agli utenti l'autorizzazione per l'esecuzione di script esterni in Machine Learning Services per SQL Server e le autorizzazioni di lettura, scrittura o DDL (Data Definition Language) per i database.

Per altre informazioni, vedere la sezione sulle autorizzazioni in [Panoramica della sicurezza per il framework di estendibilità](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Autorizzazione per l'esecuzione di script

Se si è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalmente e si eseguono script R o Python in una propria istanza, per l'esecuzione di script si usano in genere diritti di amministratore. Si dispone quindi di autorizzazioni implicite per varie operazioni e per tutti i dati nel database.

La maggior parte degli utenti, tuttavia, non ha autorizzazioni così elevate. Ad esempio, gli utenti di un'organizzazione che usano account di accesso SQL per accedere al database in genere non hanno autorizzazioni elevate. È quindi necessario concedere l'autorizzazione per l'esecuzione di script esterni in ogni database in cui viene usato il linguaggio a ogni utente di Machine Learning Services che usa R o Python. Ecco come:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Le autorizzazioni non sono specifiche del linguaggio di scripting supportato. In altre parole, non esistono livelli di autorizzazione separati per script R e script Python. Se è necessario gestire autorizzazioni separate per questi linguaggi, installare R e Python in istanze separate.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Concedere autorizzazioni per i database

Mentre esegue alcuni script, un utente può avere bisogno di leggere dati da altri database, nonché di creare nuove tabelle per archiviare i risultati e scrivere dati nelle tabelle.

Assicurarsi che ogni account utente e ogni account di accesso SQL Windows che esegue script R o Python abbia le autorizzazioni appropriate per il database specifico: `db_datareader` per leggere i dati, `db_datawriter` per salvare oggetti nel database o `db_ddladmin` per creare oggetti, ad esempio stored procedure o tabelle, in cui inserire dati sottoposti a training e serializzati.

L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente, ad esempio, concede all'account di accesso SQL *MySQLLogin* i diritti per l'esecuzione di query T-SQL nel database *ML_Samples*. Per eseguire questa istruzione, l'account di accesso SQL deve essere già presente nel contesto di sicurezza del server.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle autorizzazioni incluse in ogni ruolo, vedere [Ruoli a livello di database](../../relational-databases/security/authentication-access/database-level-roles.md).