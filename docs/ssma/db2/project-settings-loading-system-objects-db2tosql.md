---
title: Impostazioni (caricamento oggetti di sistema) del progetto (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 65f9070aabc6f64e1fc327abe67e595696c04423
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63266455"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Impostazioni (caricamento oggetti di sistema) del progetto (DB2ToSQL)
La pagina di caricamento di oggetti di sistema dei **impostazioni del progetto** finestra di dialogo consente di specificare quali oggetti di sistema DB2 SSMA converte e carica in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Nel riquadro di caricamento di oggetti di sistema è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo:  
  
-   Per specificare le impostazioni per tutti i progetti SSMA, il **strumenti** dal menu **impostazioni di progetto predefinite**, selezionare il tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati da **Versione di destinazione della migrazione** elenco a discesa fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi fare clic su **il caricamento di oggetti di sistema**.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu **le impostazioni del progetto**, fare clic su **generale** nella parte inferiore del riquadro di sinistra e quindi fare clic su **Caricamento di oggetti di sistema**.  
  
## <a name="default-settings"></a>Impostazioni predefinite  
Conversione di oggetti di sistema utilizza le risorse di sistema e richiede tempo. Per migliorare le prestazioni, SSMA consente di selezionare solo gli oggetti di sistema usate più di frequente, come illustrato nel seguente elenco:  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS.STANDARD  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
Se gli oggetti di DB2 fanno riferimento agli oggetti di sistema aggiuntive, è necessario selezionare gli oggetti. Se non si seleziona gli oggetti di sistema che fanno riferimento gli oggetti di database di DB2, SSMA segnalerà gli errori di conversione. Se si ricevono errori di conversione causati dalla mancanza di oggetti di sistema, selezionare gli oggetti mancanti nella finestra di dialogo. È quindi possibile ripetere la conversione in base alle esigenze.  
  
