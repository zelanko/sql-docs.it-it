---
title: Riferimenti alle librerie ADO In un'applicazione Visual Basic 6 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8e37459c5e48fe817a3bdbb6a824550cf977f66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222038"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Riferimenti alle librerie ADO in un'applicazione Visual Basic 6
Per importare le librerie ADO in un'applicazione di Microsoft Visual Basic 6, è necessario impostare un riferimento nel progetto di Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Per impostare un riferimento alle librerie ADO in un progetto Visual Basic  
  
1.  Creare un nuovo o aprire un progetto di Visual Basic esistente.  
  
2.  Scegliere il **Project** voce di menu e quindi selezionare **riferimenti...**  dal Pannello di riepilogo.  
  
3.  Dal **riferimenti disponibili**, selezionare la casella **Microsoft ActiveX Data Objects *n* libreria**, dove ***n*** rappresenta la versione più recente numero di versione. Il **ubicazione** campo sottostante debba identificare la scelta come *$installDir\msado15.dll*, dove *$installDir* rappresenta il percorso della directory in cui la libreria ADO è stato installato.  
  
4.  Se si prevede di utilizzare ADO MD, ripetere il passaggio 3 selezionare **Microsoft ActiveX Data Objects (multidimensionale) *n* libreria**. Il **ubicazione** campo deve identificare questa scelta come *$installDir\msadomd.dll*.  
  
5.  Se si prevede di usare ADOX, ripetere il passaggio 3 selezionare **Microsoft ADO ext *n* per la sicurezza e DDL**. Il **ubicazione** campo deve identificare questa scelta come *$installDir\msadox.dll*.  
  
6.  Fare clic su **OK** per completare l'impostazione di riferimenti.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Installazione di ADO copia anche librerie dei tipi seguenti di versioni precedenti:  
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 Type Library  
  
-   *msado21.tlb*, ADO 2.1 Type Library  
  
-   *msado20.tlb*, ADO 2.0 Type Library  
  
 Se l'applicazione deve usare uno qualsiasi di queste librerie ADO per motivi di compatibilità con le versioni precedenti, è necessario importare la versione appropriata della libreria dei tipi. A tale scopo, seguire le procedure descritte nella sezione precedente, sostituendo *msado15.dll* dal *msadoXX.tlb*, dove *XX* rappresenta il numero di versione da importare.
