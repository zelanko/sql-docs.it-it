---
title: Using the RenderedOutputFile Class for a Delivery Extension (Uso della classe RenderedOutputFile per un'estensione per il recapito) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1dcbf250a367326e5cad528384e533a9ac9d945b
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154168"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Utilizzo della classe RenderedOutputFile per un'estensione per il recapito
  La classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> rappresenta un flusso di dati e le informazioni sulle proprietà associate al flusso. La proprietà **Data** della classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> viene usata per rappresentare un report visualizzabile o una risorsa del report come un oggetto **Stream**.  
  
 Il metodo <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> dell'oggetto **Report** restituisce una matrice di uno o più oggetti <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> che insieme costituiscono un singolo report visualizzabile. Il primo oggetto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> è il report visualizzabile. Tutti gli altri oggetti <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> sono risorse che devono essere recapitate insieme ai dati del report (ad esempio, un file HTML e le immagini associate). Le estensioni per il rendering a flusso singolo (IMAGE, PDF, MHTML ed EXCEL) restituiscono solo un oggetto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> nella matrice.  
  
 Per un esempio su come usare la classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>, vedere [ Esempi del prodotto Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
