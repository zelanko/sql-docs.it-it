---
title: Impostazioni progetto (caricamento oggetti di sistema) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a5e8feb6c083c787d877cbc5491c533b8a35d740
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266615"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Impostazioni del progetto (caricamento oggetti di sistema) (OracleToSQL)
La pagina caricamento oggetti di sistema della finestra di dialogo **Impostazioni progetto** consente di specificare quali oggetti di sistema Oracle SSMA converte e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carica in.  
  
Il riquadro caricamento oggetti di sistema è disponibile nelle finestre di dialogo **Impostazioni** progetto e **Impostazioni progetto predefinite** :  
  
-   Per specificare le impostazioni per tutti i progetti SSMA, nel menu **strumenti** selezionare **Impostazioni progetto predefinite**, selezionare il tipo di progetto di migrazione per il quale le impostazioni devono essere visualizzate o modificate dall'elenco a discesa **versione destinazione migrazione** fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **carica oggetti di sistema**.  
  
-   Per specificare le impostazioni per il progetto corrente, scegliere **Impostazioni progetto**dal menu **strumenti** , fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **carica oggetti di sistema**.  
  
## <a name="default-settings"></a>Impostazioni predefinite  
La conversione di oggetti di sistema utilizza risorse di sistema e richiede tempo. Per migliorare le prestazioni, SSMA seleziona solo gli oggetti di sistema usati più di frequente, come illustrato nell'elenco seguente:  
  
-   SYS. DBMS_OUTPUT  
  
-   SYS. DBMS_PIPE  
  
-   SYS. DBMS_UTILITY  
  
-   SYS. STANDARD  
  
-   SYS. UTL_FILE  
  
-   SYS. DBMS_LOB  
  
-   SYS. DBMS_SQL  
  
-   SYS. DBMS_SESSION  
  
Se gli oggetti Oracle fanno riferimento a oggetti di sistema aggiuntivi, è necessario selezionare tali oggetti. Se non si selezionano gli oggetti di sistema a cui fanno riferimento gli oggetti di database Oracle, SSMA segnalerà gli errori di conversione. Se vengono visualizzati errori di conversione causati da oggetti di sistema mancanti, selezionare gli oggetti mancanti in questa finestra di dialogo. È quindi possibile ripetere la conversione se necessario.  
  
