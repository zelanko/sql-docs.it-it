---
title: Sviluppo di un'attività personalizzata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f597ee3a063da534267f7d4674a024a8fcc02f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62896142"
---
# <a name="developing-a-custom-task"></a>Sviluppo di un'attività personalizzata
  In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] vengono utilizzate attività per eseguire unità di lavoro a supporto dell'estrazione, della trasformazione e del caricamento dei dati. In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] è inclusa una varietà di attività per l'esecuzione delle azioni più frequenti, dall'esecuzione di un'istruzione SQL al download di un file da un sito FTP. Se le attività incluse e le azioni supportate non soddisfano completamente specifici requisiti, è possibile creare un'attività personalizzata.  
  
 A tale scopo, è necessario creare una classe che eredita dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, applicare l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> alla nuova classe ed eseguire l'override dei metodi e delle proprietà importanti della classe di base, tra cui il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 In questa sezione viene descritto come creare, configurare e scrivere il codice di un'attività personalizzata e della relativa interfaccia utente personalizzata facoltativa.  
  
 [Creazione di un'attività personalizzata](creating-a-custom-task.md)  
 Viene descritto il primo passaggio, ovvero la creazione dell'attività personalizzata.  
  
 [Scrittura del codice di un'attività personalizzata](coding-a-custom-task.md)  
 Viene descritto come scrivere il codice dei principali metodi di un'attività personalizzata.  
  
 [Connessione alle origini dati in un'attività personalizzata](connecting-to-data-sources-in-a-custom-task.md)  
 Viene descritto come connettere un'attività personalizzata a un'origine dati.  
  
 [Generazione e definizione di eventi in un'attività personalizzata](raising-and-defining-events-in-a-custom-task.md)  
 Viene descritto come generare eventi e definire eventi personalizzati dall'attività personalizzata.  
  
 [Aggiunta di supporto per il debug in un'attività personalizzata](adding-support-for-debugging-in-a-custom-task.md)  
 Viene descritto come creare destinazioni di punti di interruzione nell'attività personalizzata.  
  
 [Sviluppo di un'interfaccia utente per un'attività personalizzata](developing-a-user-interface-for-a-custom-task.md)  
 Viene descritto come creare un'interfaccia utente visualizzata in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] per configurare le proprietà nell'attività personalizzata.  
  
## <a name="related-sections"></a>Sezioni correlate  
  
### <a name="information-common-to-all-custom-objects"></a>Informazioni comuni per tutti gli oggetti personalizzati  
 Per informazioni comuni a tutti i tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di oggetti personalizzati per Integration Services](../developing-custom-objects-for-integration-services.md)  
 Vengono descritti i passaggi di base per implementare tutti i tipi di oggetti personalizzati in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistenza degli oggetti personalizzati](../persisting-custom-objects.md)  
 Viene descritta la persistenza personalizzata e vengono illustrati i casi in cui è necessaria.  
  
 [Compilazione, distribuzione e debug di oggetti personalizzati](../building-deploying-and-debugging-custom-objects.md)  
 Vengono descritte le tecniche per la compilazione, la firma, la distribuzione e il debug di oggetti personalizzati.  
  
### <a name="information-about-other-custom-objects"></a>Informazioni su altri oggetti personalizzati  
 Per informazioni sugli altri tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di una gestione connessione personalizzata](../connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto come programmare gestioni connessioni personalizzate.  
  
 [Sviluppo di un provider di log personalizzato](../log-provider/developing-a-custom-log-provider.md)  
 Viene descritto come programmare provider di log personalizzati.  
  
 [Sviluppo di un enumeratore Foreach personalizzato](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Viene descritto come programmare enumeratori personalizzati.  
  
 [Sviluppo di un componente flusso di dati personalizzato](../data-flow/developing-a-custom-data-flow-component.md)  
 Viene descritto come programmare origini, trasformazioni e destinazioni personalizzate del flusso di dati.  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedi anche  
 [Estensione del pacchetto con l'attività script](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
