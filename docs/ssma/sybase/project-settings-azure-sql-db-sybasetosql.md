---
title: Impostazioni progetto (database SQL di Azure) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b79d4e94126676e128d803176463b314348ed8a1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930922"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>Impostazioni progetto (database SQL di Azure) (SybaseToSQL)
Le impostazioni del progetto del database SQL di Azure consentono di configurare il suffisso del database SQL di Azure da aggiungere nella finestra di dialogo di connessione e consentire anche l'implementazione del meccanismo heartbeat nella connessione al database SQL di Azure.  
  
Il riquadro database SQL di Azure è disponibile nelle finestre di dialogo **Impostazioni progetto** e **Impostazioni progetto predefinite** .  
  
-   Utilizzare la finestra di dialogo Impostazioni progetto per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni del database SQL di Azure, nel menu **strumenti** selezionare **Impostazioni progetto**, fare clic su **generale** nella parte inferiore del riquadro a sinistra e quindi selezionare **database SQL di Azure**.  
  
-   Utilizzare la finestra di dialogo Impostazioni progetto predefinite per impostare le opzioni di configurazione per tutti i progetti. Per accedere alle impostazioni del database SQL di Azure, nel menu **strumenti** selezionare **Impostazioni DefaultProject**, fare clic su **generale** nella parte inferiore del riquadro a sinistra e quindi selezionare **database SQL di Azure**.  
  
## <a name="connectivity"></a>Connettività  
**Intervallo heartbeat**  
  
Specifica un intervallo di tempo da usare per il meccanismo di heartbeat per tenere attiva la connessione al database SQL di Azure nel formato "minuti: secondi".  
  
**Valore predefinito**:' 4:45'  
  
Il valore deve essere specificato nel formato ' m:SS ' (ad esempio,' 4:45' o ' 0:50').  
  
**Suffisso del server del database SQL di Azure**  
  
Specifica un suffisso del server del database SQL di Azure  
  
**Valore predefinito**:' database.Windows.NET '.  
  
