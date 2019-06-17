---
title: Impostazioni progetto (database SQL di Azure) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2307a62c05503a231c3ee16b79efb25e964f55bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453473"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>Impostazioni progetto (database SQL di Azure) (AccessToSQL)
Le impostazioni del progetto di SQL Azure consentono di configurare il suffisso del database SQL Azure da aggiungere nella finestra di dialogo di connessione e consente inoltre l'implementazione di meccanismo di heartbeat in connessione SQL Azure.  
  
Nel riquadro SQL Azure è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni di SQL Azure, nel **degli strumenti** dal menu **le impostazioni del progetto**, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **SQL Azure**.  
  
-   Utilizzare la finestra di dialogo Impostazioni di progetto predefinito per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di SQL Azure, scegliere il **strumenti** dal menu **DefaultProject impostazioni**, selezionare il tipo di progetto come "SQL Azure" in **versione di destinazione della migrazione** della casella combinata accedere alle impostazioni nel riquadro SQL Azure, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **di SQL Azure**.  
  
## <a name="options"></a>Opzioni  
  
## <a name="connectivity"></a>Connettività  
**Intervallo di heartbeat**  
  
Specifica un intervallo di tempo da utilizzare per il meccanismo di heartbeat per mantenere la connessione di SQL Azure attivo in ' minuti: formato secondi.  
  
**Il valore predefinito**:' 4:45 '  
  
Il valore deve essere specificato in sto: formato degli ss (ad esempio, ' 4:45 ' o ' 0:50 ').  
  
**Suffisso di Server SQL Azure**  
  
Specifica il suffisso del server SQL Azure  
  
**Il valore predefinito**: 'database.windows.net'.  
  
