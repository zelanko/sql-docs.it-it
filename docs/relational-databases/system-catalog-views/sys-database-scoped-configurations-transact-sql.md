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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: 372d3a1b5722b1a19e9560fe92f61e45b6744ace
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78180106"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys. database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Contiene una riga per ogni configurazione. 

|Nome colonna|Tipo di dati|Descrizione|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|ID dell'opzione di configurazione.|
|**nome**|**nvarchar (60)**|Nome dell'opzione di configurazione. Per informazioni sulle possibili configurazioni, vedere [ALTER database scoped CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**value**|**SqlVariant**|Valore impostato per questa opzione di configurazione per la replica primaria.|
|**value_for_secondary**|**SqlVariant**|Valore impostato per questa opzione di configurazione per le repliche secondarie.|
|**is_value_default**|**bit** |Specifica se il valore impostato è il valore predefinito.|
|**dw_compatibility_level**|**int**|Livello di compatibilità del database.  Valore predefinito = 0 (automatico)|

## <a name="Permissions"></a> Autorizzazioni

È richiesta l'appartenenza al ruolo **public** .

## <a name="remarks"></a>Osservazioni

Quando viene restituito NULL come valore per **value_for_secondary**, significa che la replica secondaria è impostata su Primary.
 
Le impostazioni di configurazione con ambito database saranno trasferite insieme al database. Ciò significa che quando un database viene ripristinato o collegato, le impostazioni di configurazione esistenti non vengono modificate.

## <a name="see-also"></a>Vedere anche

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
