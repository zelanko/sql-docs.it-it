---
title: Raccolta dati nel controllo ReportViewer 2016
uthor: markingmyname
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: 69d37c54e49943807c35102362f161e2dbf23068
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2019
ms.locfileid: "66823002"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrazione di Reporting Services tramite i controlli ReportViewer - Raccolta dati

Il controllo raccoglie dati di utilizzo anonimi per una miglior interpretazione delle modalità d'uso del prodotto da parte dei clienti. I dati di utilizzo consentono di concentrare le fasi di sviluppo future sui miglioramenti più importanti per i clienti.

Una spiegazione delle procedure di raccolta e utilizzo dei dati di Microsoft SQL Server e Visualizzatore report è disponibile nell'[Informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="opting-out-of-data-collection"></a>Rifiuto esplicito della raccolta dati

È possibile disabilitare la raccolta dei dati di utilizzo tramite la proprietà ```EnableTelemetry```.

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

In alternativa è possibile disabilitarla direttamente prima del rendering del controllo.
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Vedere anche

[Uso del controllo Web Form Visualizzatore report](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrazione di Reporting Services tramite i controlli Visualizzatore report](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



