---
title: Implementazione di una classe Command per un'estensione per l'elaborazione dati | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e415d9498c624aa3dcea443f2cdc3641dd7c8491
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193948"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>Implementazione di una classe Command per un'estensione per l'elaborazione dati
  L'oggetto **Command** formula una richiesta e la passa all'origine dati. Il testo del comando può avere forme sintattiche diverse, tra cui testo e XML. Se vengono restituiti risultati, l'oggetto **Command** restituisce i risultati come oggetto **DataReader**.  
  
 Per creare una classe **Command**, implementare <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>. Implementare il metodo <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> per restituire un set di risultati come oggetto **DataReader**. Il metodo <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> della classe **Command** deve includere un'implementazione che accetti un'enumerazione <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> come argomento. Se si distribuisce l'estensione per l'elaborazione dati in Progettazione report, fornire un'implementazione in grado di gestire un caso <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> nel metodo <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>. Un'implementazione di solo schema viene utilizzata per fornire un elenco di campi a Progettazione report. L'oggetto **DataReader** restituito dal metodo <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> deve contenere informazioni relative a tipo e nome per i campi, o le colonne, del set di risultati.  
  
 Facoltativamente, la classe **Command** può implementare <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>. Questa interfaccia consente a una classe di implementazione di analizzare una query e restituire un elenco di parametri della query. La funzionalità dell'interfaccia <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> viene utilizzata solo in Progettazione report. Quando si implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>, si consente agli utenti di Progettazione report di ricevere una richiesta per i parametri ogni volta che un report viene eseguito in modalità di anteprima. È anche possibile visualizzare i parametri nella scheda **Parametri** della finestra di dialogo **Set di dati**.  
  
> [!NOTE]  
>  Non implementare <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> se l'estensione per l'elaborazione dati personalizzata non supporta i parametri.  
  
 Per un'implementazione di esempio della classe **Command**, vedere la pagina degli [esempi del prodotto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
