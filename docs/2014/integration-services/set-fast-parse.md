---
title: Imposta analisi veloce | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e6ff2c6ecd536dd5ecc34dceb358ffcf578ff3a7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421728"
---
# <a name="set-fast-parse"></a>Impostazione dell'analisi veloce
  È necessario impostare la proprietà relativa all'analisi veloce per ogni colonna dell'origine o della trasformazione in cui questa viene utilizzata. Per impostare la proprietà, utilizzare l'editor avanzato dell'origine file flat e della trasformazione Conversione dati.  
  
### <a name="to-set-fast-parse"></a>Per impostare l'analisi veloce  
  
1.  Fare clic con il pulsante destro del mouse sull'origine file flat o sulla trasformazione Conversione dati e quindi scegliere **Visualizza editor avanzato**.  
  
2.  Nella finestra di dialogo **Editor avanzato** fare clic sulla scheda **Proprietà input e output** .  
  
3.  Nel riquadro **Input e output** fare clic sulla colonna per la quale si desidera abilitare l'analisi veloce.  
  
4.  Nel Finestra Proprietà espandere il nodo **proprietà personalizzate** , quindi impostare la `FastParse` proprietà su `True` .  
  
5.  Fare clic su **OK**.  
  
  
