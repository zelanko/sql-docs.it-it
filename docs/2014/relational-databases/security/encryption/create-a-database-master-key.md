---
title: Creare la chiave master di un database | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 86f74710e99079d0acd28db09bcf1e4ba7c57865
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957245"
---
# <a name="create-a-database-master-key"></a>Creazione della chiave master di un database

In questo argomento viene descritto come creare una chiave master del database `master` nel database [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] in utilizzando [!INCLUDE[tsql](../../../includes/tsql-md.md)].

**Contenuto dell'argomento**

- **Prima di iniziare:**

  [Sicurezza](#Security)

- [Per creare una chiave master del database utilizzando Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a>Prima di iniziare

### <a name="Security"></a>Sicurezza

#### <a name="Permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL per il database.

## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL

### <a name="to-create-a-database-master-key"></a>Per creare la chiave master di un database

1. Scegliere una password per la crittografia della copia della chiave master che verrà archiviata nel database.
2. In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Espandere **Database di sistema**, fare clic con il pulsante destro del mouse su `master` e quindi scegliere **Nuova query**.
4. Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Per altre informazioni, vedere [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
