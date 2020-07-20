---
title: Opzione di configurazione allow polybase export | Microsoft Docs
description: Impostare l'opzione di configurazione `allow polybase export` nelle impostazioni di SQL Server
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279650"
---
# <a name="set-allow-polybase-export-configuration-option"></a>Impostare l'opzione di configurazione `allow polybase export`

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

L'opzione di configurazione server `allow polybase export` consente le operazioni `INSERT` in una tabella esterna Hadoop. 

Questa funzionalità non supporta l'inserimento in altre origini dati esterne.

 I valori possibili sono illustrati nella tabella seguente: 

| valore | Significato                                |
|-------|----------------------------------------|
| 0     | Disabilitato. Si tratta dell'impostazione predefinita. |
| 1     | Attivato                                |


L'impostazione ha effetto immediato.

## <a name="example"></a>Esempio

Nell'esempio seguente viene abilitata questa impostazione.

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>Passaggi successivi

 [Esportazione di dati](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)