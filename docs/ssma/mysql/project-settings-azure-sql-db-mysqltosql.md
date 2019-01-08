---
title: Impostazioni progetto (database SQL di Azure) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e0c16fe617b5808f22f15cdf89af8dc7a1e79898
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410868"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Impostazioni del progetto (database SQL di Azure) (MySQLToSQL)
Le impostazioni del progetto di SQL Azure consentono di configurare il suffisso del database SQL Azure da aggiungere nella finestra di dialogo di connessione e consente inoltre l'implementazione di meccanismo di heartbeat in connessione SQL Azure.  
  
Nel riquadro SQL Azure è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni di SQL Azure, nel **degli strumenti** dal menu **le impostazioni del progetto**, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **SQL Azure**.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto predefinito per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di SQL Azure, scegliere il **strumenti** dal menu **DefaultProject impostazioni**, selezionare il tipo di progetto di migrazione come SQL Azure da **versione di destinazione della migrazione** drop fino a accesso le impostazioni nel riquadro SQL Azure, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **di SQL Azure**.  
  
## <a name="options"></a>Opzioni  
  
## <a name="connectivity"></a>Connettività  
**Intervallo di heartbeat**  
  
Specifica un intervallo di tempo da utilizzare per il meccanismo di heartbeat per mantenere la connessione di SQL Azure attivo in ' minuti: formato secondi.  
  
**Il valore predefinito**:' 4:45 '  
  
Il valore deve essere specificato in sto: formato degli ss (ad esempio, ' 4:45 ' o ' 0:50 ').  
  
**Suffisso di Server SQL Azure**  
  
Specifica il suffisso del server SQL Azure  
  
**Il valore predefinito**: 'database.windows.net'.  
  
