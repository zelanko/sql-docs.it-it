---
title: Impostazioni globali (finestre di dialogo) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: a85eb72b3c239b8be0141c445e5d4507efb438cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192348"
---
# <a name="global-settings-dialogs--oracletosql"></a>Global Settings (Dialogs)  (OracleToSQL)
Utilizzare la pagina di finestre di dialogo del **Global Settings** finestra di dialogo per specificare l'azione predefinita dell'utente e le impostazioni di avviso per SSMA.  
  
Per accedere alle impostazioni della finestra di dialogo nel **degli strumenti** dal menu **impostazioni globali**, fare clic su **GUI** nella parte inferiore del riquadro a sinistra e quindi selezionare **finestre di dialogo**.  
  
## <a name="options"></a>Opzioni  
**Avvisa prima di sovrascrivere gli oggetti**  
Quando SSMA converte gli oggetti in SQL Server, alcuni oggetti potrebbero già esistere in metadati del Server SQL del progetto. Questi oggetti potrebbero sono già stati convertiti, o gli oggetti abbiano semplicemente lo stesso nome dello schema di destinazione come oggetti che si desidera convertire.  
  
Usare questa opzione per specificare se SSMA venga chiesto di sovrascrivere le definizioni degli oggetti duplicati:  
  
-   Se si seleziona **True**, SSMA visualizzerà una finestra di dialogo di avviso quando rileva un oggetto duplicato. In questa finestra di dialogo è possibile specificare per sovrascrivere i singoli oggetti o tutti gli oggetti duplicati o per ignorare tutti gli oggetti duplicati o singoli oggetti.  
  
-   Se si seleziona **False**, il **azione predefinita di sovrascrittura dell'oggetto** opzione viene visualizzata in cui si specifica l'azione predefinita.  
  
**Azione predefinita di sovrascrittura di oggetto**  
Questa opzione viene visualizzata se si seleziona **False** per il **Avvisa prima di sovrascrivere gli oggetti** opzione.  
  
Usare questa opzione per specificare l'oggetto predefinito comportamento di sovrascrittura:  
  
-   Se si seleziona **True**, SSMA sovrascriverebbe automaticamente gli oggetti nei metadati del progetto di SQL Server con lo stesso nome e lo stesso schema di destinazione dell'oggetto da convertire.  
  
-   Se si seleziona **False**, SSMA non sovrascrive i metadati degli oggetti durante la conversione.  
  
