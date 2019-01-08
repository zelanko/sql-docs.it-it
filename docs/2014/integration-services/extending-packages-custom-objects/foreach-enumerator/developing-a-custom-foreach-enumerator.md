---
title: Sviluppo di un enumeratore Foreach personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7282608351cd956bc5f3a918147d5ec6184bfdf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377473"
---
# <a name="developing-a-custom-foreach-enumerator"></a>Sviluppo di un enumeratore Foreach personalizzato
  In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] gli enumeratori Foreach vengono utilizzati per scorrere gli elementi di una raccolta ed eseguire le stesse attività per ogni elemento. In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] è inclusa una varietà di enumeratori Foreach che supportano le raccolte più comunemente utilizzate, ad esempio tutti i file di una cartella, tutte le tabelle di un database o tutti gli elementi di un elenco archiviato in una variabile del pacchetto. Se gli enumeratori Foreach e le raccolte disponibili non soddisfano completamente specifici requisiti, è possibile creare un enumeratore Foreach personalizzato.  
  
 A tale scopo, è necessario creare una classe che eredita dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, applicare l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> alla nuova classe ed eseguire l'override dei metodi e delle proprietà importanti della classe di base, tra cui il metodo <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
## <a name="in-this-section"></a>In questa sezione  
 In questa sezione viene descritto come creare, configurare e scrivere il codice di un enumeratore Foreach personalizzato e della relativa interfaccia utente personalizzata.  
  
 [Creazione di un enumeratore Foreach personalizzato](creating-a-custom-foreach-enumerator.md)  
 Viene descritto come creare le classi per un progetto di enumeratore Foreach personalizzato.  
  
 [Scrittura del codice di un enumeratore Foreach personalizzato](coding-a-custom-foreach-enumerator.md)  
 Viene descritto come implementare un enumeratore Foreach personalizzato eseguendo l'override dei metodi e delle proprietà della classe di base.  
  
 [Sviluppo di un'interfaccia utente per un enumeratore Foreach personalizzato](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 Viene descritto come implementare la classe dell'interfaccia utente e il form utilizzato per configurare l'enumeratore Foreach personalizzato.  
  
## <a name="related-topics"></a>Argomenti correlati  
  
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
  
 [Sviluppo di un'attività personalizzata](../task/developing-a-custom-task.md)  
 Viene descritto come programmare attività personalizzate.  
  
 [Sviluppo di una gestione connessione personalizzata](../connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto come programmare gestioni connessioni personalizzate.  
  
 [Sviluppo di un provider di log personalizzato](../log-provider/developing-a-custom-log-provider.md)  
 Viene descritto come programmare provider di log personalizzati.  
  
 [Sviluppo di un componente flusso di dati personalizzato](../data-flow/developing-a-custom-data-flow-component.md)  
 Viene descritto come programmare origini, trasformazioni e destinazioni personalizzate del flusso di dati.  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
