---
title: Sviluppo di tipi specifici di componenti del flusso di dati | Microsoft Docs
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
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0092a86412e5b9d33d53dbc79ff2c4770d8c10e4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354830"
---
# <a name="developing-specific-types-of-data-flow-components"></a>Sviluppo di tipi specifici di componenti del flusso di dati
  In questa sezione vengono descritte le specifiche dello sviluppo di componenti di origine, componenti di trasformazione con output sincroni, componenti di trasformazione con output asincroni e componenti di destinazione.  
  
 Per informazioni sullo sviluppo di componenti flusso dati in generale, vedere [Sviluppo di un componente flusso di dati personalizzato](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Sviluppo di un componente di origine personalizzato](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contiene informazioni sullo sviluppo di un componente che accede ai dati da un'origine dati esterna e li fornisce ai componenti a valle nel flusso di dati.  
  
 [Sviluppo di un componente di trasformazione personalizzato con output sincroni](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contiene informazioni sullo sviluppo di un componente di trasformazione i cui output sono sincroni con gli input. Questi componenti non aggiungono dati al flusso di dati, ma li elaborano mentre passano.  
  
 [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contiene informazioni sullo sviluppo di un componente di trasformazione i cui output non sono sincroni con gli input. Questi componenti ricevono dati dai componenti a monte, ma aggiungono anche dati al flusso di dati.  
  
 [Sviluppo di un componente di destinazione personalizzato](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contiene informazioni sullo sviluppo di un componente che riceve righe dai componenti a monte nel flusso di dati e li scrive in un'origine dati esterna.  
  
## <a name="reference"></a>Riferimenti  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene le classi e le interfacce utilizzate per creare componenti del flusso di dati personalizzati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene le classi e le interfacce non gestite dell'attività Flusso di dati. Lo sviluppatore utilizza questi oggetti e lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Pipeline> gestito quando compila un flusso di dati a livello di programmazione o crea componenti del flusso di dati personalizzati.  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Sviluppo di tipi specifici di componenti script](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
