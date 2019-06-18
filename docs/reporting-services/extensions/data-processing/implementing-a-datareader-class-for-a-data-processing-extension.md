---
title: Implementazione di una classe DataReader per un'estensione per l'elaborazione dati | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1367774e84dd10c2749f46a1ee6c38b8d5f6dd7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193914"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Implementazione di una classe DataReader per un'estensione per l'elaborazione dati
  L'oggetto **DataReader** consente a un client di recuperare da un'origine dati un flusso di dati forward-only di sola lettura. I risultati vengono restituiti quando la query viene eseguita e vengono archiviati nel buffer di rete nel client fino a quando non vengono richiesti tramite il metodo **Read** della classe **DataReader**. Per creare una classe **DataReader**, implementare <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e, facoltativamente, <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. L'uso di un oggetto **DataReader** migliora le prestazioni dell'applicazione consentendo di recuperare i dati non appena sono disponibili senza attendere che vengano restituiti tutti i risultati della query nonché, per impostazione predefinita, consentendo di archiviare in memoria una sola riga per volta, riducendo l'overhead di sistema.  
  
 Dopo aver creato un'istanza della classe **Command**, è possibile creare l'oggetto **DataReader** chiamando **Command.ExecuteReader** per recuperare le righe dall'origine dati. L'implementazione di **DataReader** deve offrire due funzionalità di base, ovvero l'accesso forward-only ai set di risultati ottenuti eseguendo un comando e l'accesso ai tipi di colonna, ai nomi e ai valori all'interno di ogni riga. I client usano il metodo **Read** dell'oggetto **DataReader** per ottenere una riga dai risultati della query.  
  
 In Progettazione report l'oggetto **DataReader** viene usato per recuperare un elenco di campi e le informazioni sullo schema per il set di risultati. A tale scopo, vengono implementati i metodi **GetName**, **GetValue**, **GetFieldType** e **GetOrdinal** dell'interfaccia <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>.  
  
 L'interfaccia <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> consente di fornire informazioni di aggregazione specifiche per il set di risultati. Per un'implementazione di esempio della classe **DataReader**, vedere la pagina degli [esempi del prodotto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
