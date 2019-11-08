---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530933"
---
Per alcune operazioni, inclusa la configurazione delle impostazioni del server (a livello di istanza) o l'aggiunta manuale di un database a un gruppo di disponibilità, è necessaria una connessione all'istanza di SQL Server. Per operazioni come `sp_configure`, `RESTORE DATABASE` o per qualsiasi comando DDL in un database appartenente a un gruppo di disponibilità è necessaria una connessione all'istanza di SQL Server. Per impostazione predefinita, un cluster Big Data non include un endpoint che abilita una connessione all'istanza. È necessario esporre questo endpoint manualmente.

Per istruzioni, vedere [Connessione ai database nella replica primaria](../big-data-cluster/deployment-high-availability.md#instance-connect).