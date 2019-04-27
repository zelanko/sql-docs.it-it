---
title: Concedere le autorizzazioni di database per l'esecuzione di script R e Python - servizi di SQL Server Machine Learning
description: Come concedere autorizzazioni utente del database per l'esecuzione di script R e Python in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e281f1712163aeee1846565458c2b037077c8588
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641670"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Consentire agli utenti di SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come è possibile concedere agli utenti l'autorizzazione per eseguire gli script esterni in SQL Server Machine Learning Services e concedere le autorizzazioni di language (DDL) per database di dati, scrittura o lettura definizione.

Per altre informazioni, vedere la sezione autorizzazioni negli [Panoramica sulla sicurezza per il framework di estendibilità](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Autorizzazione per eseguire gli script

Se è stato installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manualmente, mentre si eseguono gli script R o Python nella tua istanza di, è in genere eseguire gli script come amministratore. In questo modo, si dispone dell'autorizzazione implicita su varie operazioni e tutti i dati nel database.

La maggior parte degli utenti, tuttavia, si dispone di tali autorizzazioni con privilegi elevati. Ad esempio, gli utenti in un'organizzazione che usano account di accesso SQL per accedere al database in genere non è le autorizzazioni con privilegi elevate. Pertanto, per ogni utente che usa R o Python, è necessario concedere agli utenti di servizi di Machine Learning l'autorizzazione per eseguire gli script esterni in ogni database in cui viene utilizzata la lingua. Ecco come:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Autorizzazioni non sono specifiche del linguaggio di script supportato. In altre parole, non esistono livelli di autorizzazione separati per lo script R e lo script Python. Se è necessario mantenere separate le autorizzazioni per queste lingue, installare R e Python in istanze separate.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Concedere le autorizzazioni di database

Mentre un utente è in esecuzione gli script, l'utente potrebbe essere necessario leggere i dati da altri database. L'utente potrebbe essere necessario anche creare nuove tabelle per archiviare i risultati e scrivere dati nelle tabelle.

Per ogni account utente di Windows o account di accesso SQL che esegue gli script R o Python, verificare che abbia le autorizzazioni appropriate sul database specifico: `db_datareader` per leggere i dati, `db_datawriter` per salvare gli oggetti nel database, o `db_ddladmin` per creare gli oggetti ad esempio le stored procedure o tabelle contenenti sottoposto a training e i dati serializzati.

Ad esempio, il seguente [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione offre l'accesso SQL *MySQLLogin* i diritti per eseguire query T-SQL *ML_Samples* database. Per eseguire questa istruzione, l'account di accesso SQL deve essere già presente nel contesto di sicurezza del server.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle autorizzazioni incluse in ogni ruolo, vedere [ruoli a livello di Database](../../relational-databases/security/authentication-access/database-level-roles.md).