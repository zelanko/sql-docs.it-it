---
title: Raccolta dati nel controllo ReportViewer
description: Il controllo raccoglie dati di utilizzo anonimi per una miglior interpretazione delle modalità d'uso del prodotto da parte dei clienti. I dati di utilizzo consentono di concentrare le fasi di sviluppo future sui miglioramenti più importanti per i clienti.
author: maggiesMSFT
ms.author: maggies
ms.custom: ''
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 09/18/2018
ms.openlocfilehash: d7b70445fc4d8a29d8ebcdf7ecbffe4b54133f0e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796891"
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



