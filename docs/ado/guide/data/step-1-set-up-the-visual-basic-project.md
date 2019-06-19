---
title: 'Passaggio 1: Configurare il progetto di Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700606"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Passaggio 1: Configurare il progetto di Visual Basic
In questo scenario, si presuppone di disporre di Microsoft Visual Basic 6.0, ADO 2.5 o versioni successive e il Provider Microsoft OLE DB per Internet Publishing installati nel sistema. Si verrà innanzitutto creato un nuovo progetto e quindi aggiungere alcuni controlli al form predefinito nel progetto.  
  
### <a name="to-create-an-ado-project"></a>Per creare un progetto di ADO:  
  
1.  In Microsoft Visual Basic, creare un nuovo progetto Standard EXE.  
  
2.  Dal menu progetto, scegliere i riferimenti.  
  
3.  Selezionare "Libreria Microsoft ActiveX Data Objects 2.5" e fare clic su OK.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Per inserire i controlli nel form principale:  
  
1.  Aggiungere un controllo ListBox a Form1. Impostarne la proprietà nome su **lstMain**.  
  
2.  Aggiungere un altro controllo ListBox a Form1. Impostarne la proprietà nome su **lstDetails**.  
  
3.  Aggiungere un controllo TextBox a Form1. Impostarne la proprietà nome su **txtDetails**.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Passaggio 2: Inizializzare la casella di riepilogo principale](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
