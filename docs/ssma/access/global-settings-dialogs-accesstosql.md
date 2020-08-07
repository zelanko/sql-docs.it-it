---
title: Impostazioni globali (finestre di dialogo) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5424bb29fa88b36e1cd12dd915586080d99d2e47
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938441"
---
# <a name="global-settings-dialogs-accesstosql"></a>Impostazioni globali (finestre di dialogo) (AccessToSQL)
Utilizzare la pagina finestre di dialogo della finestra di dialogo **Impostazioni globali** per specificare le impostazioni predefinite per l'azione e l'avviso dell'utente per SSMA.  
  
Per accedere alle impostazioni della finestra di dialogo nel menu **strumenti** , selezionare **Impostazioni globali**, fare clic su **GUI** nella parte inferiore del riquadro a sinistra e quindi selezionare **finestre di dialogo**.  
  
## <a name="options"></a>Opzioni  
**Mostra migrazione guidata all'avvio**  
In SSMA per l'accesso è possibile abilitare o disabilitare la **migrazione guidata** all'avvio dell'applicazione SSMA. Per impostazione predefinita, questa opzione è impostata su **true**.  
  
-   Se l'opzione è impostata su **true**, la finestra di dialogo della migrazione guidata viene visualizzata inizialmente quando si apre SSMA per l'applicazione di accesso.  
  
-   Se l'opzione è impostata su **false**, la migrazione guidata non viene visualizzata e sarà necessario accedervi manualmente dal menu **file** , se necessario.  
  
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
  
