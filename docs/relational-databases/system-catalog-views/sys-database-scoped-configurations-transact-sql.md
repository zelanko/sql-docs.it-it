---
title: sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da115c8d4cf48cfbcd6190c88a83bee4e61ae5a1
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240763"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys. database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Contiene una riga per ogni configurazione. 

|Nome colonna|Tipo di dati|Description|
|-----------------|---------------|-----------------|
|**configuration_id**|**Int**|ID dell'opzione di configurazione.|
|**name**|**nvarchar(60)**|Nome dell'opzione di configurazione. Per informazioni sulle possibili configurazioni, vedere [ALTER database scoped Configuration &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**Valore**|**SqlVariant**|Valore impostato per questa opzione di configurazione per la replica primaria.|
|**value_for_secondary**|**SqlVariant**|Valore impostato per questa opzione di configurazione per le repliche secondarie.|
|**is_value_default**|**bit** |Specifica se il valore impostato è il valore predefinito.|

## <a name="Permissions"></a> Permissions

È richiesta l'appartenenza al ruolo **public** .

## <a name="remarks"></a>Remarks

Quando viene restituito NULL come valore per **value_for_secondary**, questo significa che la replica secondaria è impostata su Primary.
 
Le impostazioni di configurazione con ambito database saranno trasferite insieme al database. Ciò significa che quando un database viene ripristinato o collegato, le impostazioni di configurazione esistenti non vengono modificate.

## <a name="see-also"></a>Vedere anche

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
