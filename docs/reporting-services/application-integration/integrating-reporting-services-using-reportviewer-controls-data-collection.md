---
title: Raccolta dati nel controllo ReportViewer
description: ReportViewer raccoglie dati sull'utilizzo anonimi per comprendere in che modo i clienti usano il prodotto e concentrare le attività di sviluppo sui miglioramenti più rilevanti per i clienti.
author: maggiesMSFT
ms.author: maggies
ms.custom: ''
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 09/18/2018
ms.openlocfilehash: 078b36034d48dbb4389c69e64d8b8b18d240b24c
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198178"
---
# <a name="integrate-reporting-services-using-reportviewer-controls---data-collection"></a>Integrare Reporting Services usando i controlli ReportViewer - Raccolta dati

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



