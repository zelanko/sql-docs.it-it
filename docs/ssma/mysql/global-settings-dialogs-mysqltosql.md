---
description: Impostazioni globali (finestre di dialogo) (MySQLToSQL)
title: Impostazioni globali (finestre di dialogo) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e902927b90ff868e8766b3eb1fe9839938dd8ece
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463416"
---
# <a name="global-settings-dialogs-mysqltosql"></a>Impostazioni globali (finestre di dialogo) (MySQLToSQL)
Utilizzare la pagina finestre di dialogo della finestra di dialogo **Impostazioni globali** per specificare le impostazioni predefinite per l'azione e l'avviso dell'utente per SSMA.  
  
Per accedere alle impostazioni della finestra di dialogo nel menu **strumenti** , selezionare **Impostazioni globali**, fare clic su **GUI** nella parte inferiore del riquadro a sinistra e quindi selezionare **finestre di dialogo**.  
  
## <a name="options"></a>Opzioni  
**Avvisa prima di sovrascrivere oggetti**  
Quando SSMA converte gli oggetti in SQL Server, è possibile che alcuni oggetti esistano già nei metadati SQL Server del progetto. Questi oggetti potrebbero essere già stati convertiti oppure gli oggetti possono avere lo stesso nome nello schema di destinazione come oggetti da convertire.  
  
Usare questa opzione per specificare se SSMA deve richiedere la sovrascrittura delle definizioni di oggetti duplicati:  
  
-   Se si seleziona **true**, in SSMA verrà visualizzata una finestra di dialogo di avviso quando viene rilevato un oggetto duplicato. In questa finestra di dialogo è possibile specificare di sovrascrivere singoli oggetti o tutti gli oggetti duplicati oppure ignorare singoli oggetti o tutti gli oggetti duplicati.  
  
-   Se si seleziona **false**, viene visualizzata l'opzione **Sovrascrivi azione predefinita** per l'oggetto in cui viene specificata l'azione predefinita.  
  
**Azione predefinita Sovrascrivi oggetto**  
Questa opzione viene visualizzata se si seleziona **false** per l'opzione **Avvisa prima di sovrascrivere oggetti** .  
  
Usare questa opzione per specificare il comportamento predefinito di sovrascrittura dell'oggetto:  
  
-   Se si seleziona **true**, SSMA sovrascriverà automaticamente gli oggetti nei metadati del progetto SQL Server con lo stesso nome e si troveranno nello stesso schema di destinazione dell'oggetto da convertire.  
  
-   Se si seleziona **false**, SSMA non sovrascrive i metadati degli oggetti durante la conversione.  
  
