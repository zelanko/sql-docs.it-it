---
title: Editor trasformazione UnPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8bb4a435d88ea867c2152d71afb87cdd731f452e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58383870"
---
# <a name="unpivot-transformation-editor"></a>Editor trasformazione UnPivot
  Utilizzare la finestra di dialogo **Editor trasformazione UnPivot** per selezionare le colonne da trasformare in righe tramite Pivot e specificare la colonna di dati e la nuova colonna di output per il valore pivot.  
  
> [!NOTE]  
>  Per illustrare l'uso delle opzioni, questo argomento si basa sullo scenario UnPivot descritto in [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md) .  
  
 Per ulteriori informazioni sulla trasformazione tramite UnPivot, vedere [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di specificare le colonne da trasformare in righe tramite Pivot utilizzando le caselle di controllo.  
  
 **Name**  
 Consente di visualizzare il nome della colonna di input disponibile.  
  
 **Pass-through**  
 Indica se includere la colonna nell'output trasformato tramite UnPivot.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili per ogni riga. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo nella tabella **Colonne di input disponibili** .  
  
 Nello scenario UnPivot descritto in [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), le colonne di input sono le colonne **Ham**, **Soda**, **Milk**, **Beer**e **Chips** .  
  
 **Colonna di destinazione**  
 Consente di specificare un nome per la colonna di dati.  
  
 Nello scenario UnPivot descritto in [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), la colonna di destinazione è la colonna delle quantità, ovvero**Qty**.  
  
 **Valore chiave pivot**  
 Consente di specificare un nome per il valore pivot. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.  
  
 Nello scenario UnPivot descritto in [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), i valori pivot verranno visualizzati nella nuova colonna Product designata dall'opzione **Nome colonna valore chiave pivot** allo stesso modo dei valori di testo **Ham**, **Soda**, **Milk**, **Beer**e **Chips**.  
  
 **Nome colonna valore chiave pivot**  
 Consente di specificare il nome per la colonna del valore pivot. L'impostazione predefinita è "Valore chiave pivot". È comunque possibile scegliere un nome descrittivo univoco.  
  
 Nello scenario UnPivot descritto in [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), il Nome colonna valore chiave pivot è **Product** e designa la nuova colonna **Product** come la colonna in cui viene applicata la trasformazione tramite UnPivot alle colonne **Ham**, **Soda**, **Milk**, **Beer**e **Chips** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Trasformazione pivot](data-flow/transformations/pivot-transformation.md)  
  
  
