---
ms.openlocfilehash: 2dc81d434714e0a13912fa6f14e1194df5e5afe3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215614"
---
> [!NOTE]
> Quando si crea la risorsa, e periodicamente dopo la creazione, l'agente delle risorse Pacemaker imposta automaticamente il valore di `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` nel gruppo di disponibilità in base alla configurazione del gruppo di disponibilità. Se ad esempio il gruppo di disponibilità contiene tre repliche sincrone, l'agente imposterà `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` su `1`. Per informazioni dettagliate e altre opzioni di configurazione, vedere [Disponibilità elevata e protezione dati per le configurazioni del gruppo di disponibilità](../linux/sql-server-linux-availability-group-ha.md). 