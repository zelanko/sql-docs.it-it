---
description: 'Passaggio 1: Configurare il progetto di Visual Basic'
title: 'Passaggio 1: configurare il progetto Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c0c8208fa8e5352a720ef057bb54d2d0b51b923
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979542"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Passaggio 1: Configurare il progetto di Visual Basic
In questo scenario si presuppone che siano presenti Microsoft Visual Basic 6,0, ADO 2,5 o versione successiva e che Microsoft OLE DB provider for Internet Publishing sia installato nel sistema. Si creerà innanzitutto un nuovo progetto e quindi si aggiungeranno alcuni controlli al modulo predefinito nel progetto.  
  
### <a name="to-create-an-ado-project"></a>Per creare un progetto ADO:  
  
1.  In Microsoft Visual Basic creare un nuovo progetto EXE standard.  
  
2.  Scegliere riferimenti dal menu progetto.  
  
3.  Selezionare "Microsoft ActiveX Data Objects 2,5 Library" e fare clic su OK.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Per inserire i controlli nel form principale:  
  
1.  Aggiungere un controllo ListBox a Form1. Impostarne la proprietà Name su **lstMain**.  
  
2.  Aggiungere un altro controllo ListBox a Form1. Impostarne la proprietà Name su **lstDetails**.  
  
3.  Aggiungere un controllo TextBox a Form1. Impostarne la proprietà Name su **txtDetails**.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenario di pubblicazione Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Passaggio 2: Inizializzare la casella di riepilogo Main](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
