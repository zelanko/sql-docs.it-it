---
title: Opzione di configurazione del server external scripts enabled
description: Informazioni sull'opzione external scripts enabled in SQL Server. Dopo l'attivazione, è possibile eseguire script esterni nei linguaggi supportati, ad esempio R o Python.
ms.date: 06/30/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3346d217228bf6ca914b6ae1aa31af0883383908
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173242"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>Opzione di configurazione del server external scripts enabled
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Usare l'opzione **external scripts enabled** per abilitare l'esecuzione di script con determinate estensioni del linguaggio remote. Questa proprietà è DISATTIVATA per impostazione predefinita. Quando **Machine Learning Services** è installato, il programma di installazione può impostare facoltativamente questa proprietà su true.

## <a name="remarks"></a>Osservazioni

È necessario abilitare l'opzione external script enabled prima di eseguire uno script esterno usando la procedura [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . Usare **sp_execute_external_script** per eseguire script scritti in un linguaggio supportato, come R o Python. 

+ Per [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] include il supporto del linguaggio di programmazione R in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], oltre a un set di strumenti per workstation R e librerie di connettività.

    Installare la funzionalità **R Services** durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per abilitare l'esecuzione di script R.

+ Per [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] e versioni successive

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] supporta entrambi i linguaggi R e Python.

    Installare la funzionalità **Machine Learning Services** durante il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per abilitare l'esecuzione di script esterni. Durante l'installazione iniziale selezionare almeno un linguaggio di programmazione: R o Python oppure entrambi.

## <a name="additional-requirements"></a>Requisiti aggiuntivi

Dopo l'installazione, per abilitare gli script esterni eseguire lo script seguente:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

Per altre informazioni, vedere [Installare SQL Server Machine Learning Services (Python re R) in Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md) o [Linux](../../linux/sql-server-linux-setup-machine-learning-docker.md?toc=/sql/machine-learning/toc.json).

## <a name="see-also"></a>Vedere anche

+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
+ [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Documentazione per Machine Learning in SQL](../../machine-learning/index.yml)
