---
title: Impostazioni progetto (database SQL di Azure) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 14fa0cb949505ab2aeb15d1236add9acba9a1ab1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703723"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Impostazioni del progetto (database SQL di Azure) (SybaseToSQL)
Le impostazioni del progetto di database SQL di Azure consentono di configurare il suffisso di database di Azure SQL DB da aggiungere nella finestra di dialogo di connessione e consente inoltre l'implementazione di meccanismo di heartbeat nella connessione di database SQL di Azure.  
  
Nel riquadro di database SQL di Azure è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto per impostare le opzioni di configurazione per il progetto corrente. Per accedere a impostazioni di database SQL di Azure, scegliere il **strumenti** dal menu **impostazioni progetto**, fare clic su **generale** nella parte inferiore del riquadro a sinistra e quindi selezionare  **Azure SQL database**.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto predefinito per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di database SQL di Azure, scegliere il **strumenti** dal menu **DefaultProject impostazioni**, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **Azure SQL database**.  
  
## <a name="connectivity"></a>Connettività  
**Intervallo di heartbeat**  
  
Specifica un intervallo di tempo da usare per il meccanismo di heartbeat per mantenere la connessione di database SQL di Azure attiva nel ' minuti: formato secondi.  
  
**Il valore predefinito**:' 4:45 '  
  
Il valore deve essere specificato in sto: formato degli ss (ad esempio, ' 4:45 ' o ' 0:50 ').  
  
**Suffisso del Server di database SQL di Azure**  
  
Specifica un suffisso di server di database SQL di Azure  
  
**Il valore predefinito**: 'database.windows.net'.  
  
