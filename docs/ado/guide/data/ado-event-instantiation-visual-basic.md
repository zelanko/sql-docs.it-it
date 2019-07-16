---
title: 'Creazione di istanze di eventi ADO: Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ead713a37d4ecf8bdfecd0d6c485684d1ad0777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926075"
---
# <a name="ado-event-instantiation-visual-basic"></a>Creazione di istanze di eventi ADO: Visual Basic
Per gestire gli eventi ADO in Microsoft® Visual Basic®, è necessario dichiarare una variabile di a livello di modulo usando il **WithEvents** (parola chiave). La variabile può essere dichiarata solo come parte di un modulo di classe e deve essere dichiarata a livello di modulo. Questo non è più restrittivo come sembra, tuttavia, poiché Visual Basic **Form** gli oggetti sono classi. Il modo più semplice per gestire gli eventi ADO consiste nel dichiarare una variabile utilizzando **WithEvents**. L'esempio seguente viene gestito il **ConnectComplete** evento per un **connessione** oggetto:  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 Il **connessione** un oggetto dichiarato nel **Form** di livello utilizzando il **WithEvents** parola chiave per consentire la gestione degli eventi. Il gestore eventi Form_Load crea effettivamente l'oggetto tramite l'assegnazione di un nuovo **Connection** obiettare *connEvent* e quindi apre la connessione. Naturalmente, un'applicazione reale farebbe un'elaborazione più complessa nel gestore eventi Form_Load rispetto a quella illustrata di seguito.
