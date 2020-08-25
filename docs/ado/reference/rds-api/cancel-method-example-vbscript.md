---
description: Esempio del metodo Cancel (VBScript)
title: Esempio di metodo Cancel (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Cancel method [ADO], VBScript example
ms.assetid: 4ade106d-063d-486e-bc4d-a1a6b6e0bea9
author: rothja
ms.author: jroth
ms.openlocfilehash: 364f8ac8d799e8d354b43f5902eff5f3b46f4b59
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768830"
---
# <a name="cancel-method-example-vbscript"></a>Esempio del metodo Cancel (VBScript)
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Nell'esempio seguente viene illustrato come leggere il metodo [Cancel](../ado-api/cancel-method-ado.md) in fase di esecuzione. Tagliare e incollare il codice seguente nel blocco note o in un altro editor di testo e salvarlo come CancelVBS. ASP. È possibile visualizzare i risultati in qualsiasi browser client.  
  
```  
<!-- BeginCancelVBS -->  
<Script Language="VBScript">  
<!--  
Sub cmdCancelAsync_OnClick  
   ' Terminates currently running AsyncExecute,  
   ' ReadyState property set to adcReadyStateLoaded,  
   ' Recordset set to Nothing  
  ADC.Cancel  
End Sub  
  
Sub cmdRefreshTable_OnClick  
   ADC.Refresh  
End Sub  
-->  
</Script>  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="ADC">  
.  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName from Employees">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
   <PARAM NAME="Server" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
.  
</OBJECT>  
  
<TABLE DATASRC=#ADC>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<FORM>  
<INPUT type="button" value="Refresh" id=cmdRefreshTable name=cmdRefreshTable>  
<INPUT type="button" value="Cancel" id=cmdCancelAsync name=cmdCancelAsync>  
</FORM>  
<!-- EndCancelVBS -->  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Cancel (ADO)](../ado-api/cancel-method-ado.md)