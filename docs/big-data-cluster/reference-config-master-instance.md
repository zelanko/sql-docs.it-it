---
title: Proprietà di configurazione dell'istanza master di SQL Server
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per le proprietà di configurazione per l'istanza master di SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60888246623796d9b4d17c498da47ab4b6557cf2
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790448"
---
# <a name="sql-server-master-instance-configuration-properties"></a>Proprietà di configurazione dell'istanza master di SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>Proprietà

È possibile configurare le seguenti opzioni di SQL Server per l'istanza master in fase di distribuzione.

|Proprietà|Opzioni|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>Esempi

L'esempio seguente abilita SQL Server Agent e la telemetria, imposta un PID per l'edizione Enterprise e abilita il flag di traccia 1204.

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

Per istruzioni, vedere [Configurare l'istanza master di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md).

## <a name="next-steps"></a>Passaggi successivi

[Configurare l'istanza master di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)
