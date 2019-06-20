---
title: Esercitazione su RDS (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5384bfc186427231ed34e855e2fedc845aca6a66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699650"
---
# <a name="rds-tutorial-vbscript"></a>Esercitazione su RDS (VBScript)
Questo è l'esercitazione su RDS, scritto in Microsoft Visual Basic Scripting Edition. Per una descrizione dello scopo di questa esercitazione, vedere la [esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md).  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 In questa esercitazione [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) vengono creati in fase di progettazione, vale a dire, sono definiti con tag di oggetti, simile al seguente: `<OBJECT>...</OBJECT>`. In alternativa, possono essere creati in fase di esecuzione con il [metodo CreateObject (Servizi Desktop remoto)](../../../ado/reference/rds-api/createobject-method-rds.md) (metodo). Ad esempio, il **Servizi Desktop remoto. DataControl** è stato possibile creare l'oggetto simile al seguente:  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>Passaggio 1: specificare un'applicazione server  
 VBScript può scoprire il nome del server Web IIS in cui viene eseguito tramite l'accesso a VBScript **Request. ServerVariables** metodo disponibile per le pagine ASP:  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 Tuttavia, per questa esercitazione, usare il server, "server".  
  
> [!NOTE]
>  Prestare attenzione al tipo di dati di **ByRef** argomenti. VBScript non consentono di specificare il tipo di variabile, pertanto è necessario passare sempre un **Variant**. Quando si Usa HTTP, servizi desktop remoto consente di passare una variante a un metodo che prevede un non-Variant se viene richiamato con il **Servizi Desktop remoto. DataSpace** oggetti [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) (metodo). Quando si usa DCOM o un server in-process, devono corrispondere ai tipi di parametro sui lati client e server o si riceverà un errore "Mancata corrispondenza del tipo".  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>Passaggio 2a: richiamare il programma di server con Servizi Desktop remoto. DataControl  
 Questo esempio è semplicemente un commento che illustra il comportamento predefinito del **Servizi Desktop remoto. DataControl** consiste nell'eseguire la query specificata.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>Passaggio 2b: richiamare il programma di server con RDSServer  
  
## <a name="step-3---server-obtains-a-recordset"></a>Passaggio 3: Server Ottiene un Recordset  
  
## <a name="step-4---server-returns-the-recordset"></a>Passaggio 4: Server restituisce il Recordset  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>Passaggio 5: DataControl viene reso utilizzabile dai controlli di visual  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>Passaggio 6a - le modifiche vengono inviate al server con Servizi Desktop remoto. DataControl  
 Questo esempio è semplicemente un commento che illustra come il **Servizi Desktop remoto. DataControl** esegue gli aggiornamenti.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Passaggio 6b - le modifiche vengono inviate al server con RDSServer  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Questa è la fine dell'esercitazione.**  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
