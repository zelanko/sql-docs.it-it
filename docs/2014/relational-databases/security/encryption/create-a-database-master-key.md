---
title: Creare la chiave master di un database | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
ms.reviewer: carlrab
ms.openlocfilehash: cb8305d9d5a3c72e6dffafd231f21110a5abdd14
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055340"
---
# <a name="create-a-database-master-key"></a>Creazione della chiave master di un database

In questo argomento viene descritto come creare una chiave master del database nel `master` database in utilizzando [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

**Contenuto dell'articolo**

- **Prima di iniziare:**

  [Sicurezza](#Security)

- [Per creare una chiave master del database utilizzando Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare

### <a name="security"></a><a name="Security"></a> Sicurezza

#### <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni

È richiesta l'autorizzazione CONTROL per il database.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL

### <a name="to-create-a-database-master-key"></a>Per creare la chiave master di un database

1. Scegliere una password per la crittografia della copia della chiave master che verrà archiviata nel database.
2. In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Espandere **Database di sistema**, fare clic con il pulsante destro del mouse su `master` e quindi scegliere **Nuova query**.
4. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Per altre informazioni, vedere [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
