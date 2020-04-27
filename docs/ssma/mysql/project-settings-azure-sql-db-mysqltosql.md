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
ms.openlocfilehash: e4cf080d7a3bcb2d121a58a57be9f3fd41a4c18a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908823"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Impostazioni del progetto (database SQL di Azure) (MySQLToSQL)
Le impostazioni del progetto SQL Azure consentono di configurare il suffisso del database SQL Azure da aggiungere nella finestra di dialogo di connessione e di consentire anche l'implementazione del meccanismo heartbeat in SQL Azure connessione.  
  
Il riquadro SQL Azure è disponibile nelle finestre di dialogo **Impostazioni progetto** e **Impostazioni progetto predefinite** .  
  
-   Utilizzare la finestra di dialogo Impostazioni progetto per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni di SQL Azure, nel menu **strumenti** selezionare **Impostazioni progetto**, fare clic su **generale** nella parte inferiore del riquadro a sinistra e quindi selezionare **SQL Azure**.  
  
-   Utilizzare la finestra di dialogo Impostazioni progetto predefinite per impostare le opzioni di configurazione per tutti i progetti. Per accedere alle impostazioni di SQL Azure, nel menu **strumenti** selezionare **Impostazioni DefaultProject**, selezionare tipo di progetto di migrazione come SQL Azure dall'elenco a discesa **versione destinazione migrazione** per accedere alle impostazioni nel riquadro SQL Azure, fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi selezionare **SQL Azure**.  
  
## <a name="options"></a>Opzioni  
  
## <a name="connectivity"></a>Connettività  
**Intervallo heartbeat**  
  
Specifica un intervallo di tempo da usare per il meccanismo di heartbeat per tenere attiva la connessione SQL Azure nel formato "minuti: secondi".  
  
**Valore predefinito**:' 4:45'  
  
Il valore deve essere specificato nel formato ' m:SS ' (ad esempio,' 4:45' o ' 0:50').  
  
**Suffisso del server SQL Azure**  
  
Specifica il suffisso del server SQL Azure  
  
**Valore predefinito**:' database.Windows.NET '.  
  
