---
title: 'Passaggio 2: Inizializzare la casella di riepilogo principale | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0df631ccaa9cd3a6177cb4e4e8e63c65286ad361
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700370"
---
# <a name="step-2-initialize-the-main-list-box"></a>Passaggio 2: Inizializzare la casella di riepilogo Main
Per dichiarare gli oggetti globali di Record e Recordset, inserire il codice seguente (generale) (dichiarazioni) relativo a Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Questo codice dichiara riferimenti agli oggetti globale per gli oggetti di Record e Recordset che verranno utilizzati più avanti in questo scenario.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Per connettersi a un URL e popolare IstMain  
 Inserire il codice seguente nel gestore dell'evento Form Load relativo a Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Questo codice crea gli oggetti globali di Record e Recordset. L'oggetto di Record, `grec`, viene aperto con un URL specificato come ActiveConnection. Se non esiste, l'URL viene aperto. Se non esiste già, si è creato. Si noti che è necessario sostituire "<https://servername/foldername/>" con un URL valido dall'ambiente in uso.  
  
 Oggetto Recordset `grs`, viene aperto sugli elementi figlio del Record, `grec`. Quindi `lstMain` viene popolato con i nomi dei file delle risorse pubblicate per l'URL.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Passaggio 1: Configurare il progetto di Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Passaggio 3: Popolare la casella di riepilogo di campi](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
