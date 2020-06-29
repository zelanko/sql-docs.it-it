---
title: Sviluppo di tipi specifici di componenti script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec0f14ed73a8c4387e50f672f89463b4bb133e9c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426718"
---
# <a name="developing-specific-types-of-script-components"></a>Sviluppo di tipi specifici di componenti script
  Il componente script è uno strumento configurabile che è possibile utilizzare nel flusso di dati di un pacchetto per rispondere ai requisiti non soddisfatti dalle origini, dalle trasformazioni e dalle destinazioni incluse in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Questa sezione contiene esempi di codice del componente script che dimostrano le quattro opzioni disponibili per la configurazione di questo componente.  
  
-   Come origine.  
  
-   Come trasformazione con output sincroni.  
  
-   Come trasformazione con output asincroni.  
  
-   Come destinazione.  
  
 Per altri esempi del componente script, vedere [Ulteriori esempi di componente script](../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Creazione di un'origine con il componente script](creating-a-source-with-the-script-component.md)  
 Viene descritto e illustrato come creare un'origine del flusso di dati tramite il componente script.  
  
 [Creazione di una trasformazione sincrona con il componente script](creating-a-synchronous-transformation-with-the-script-component.md)  
 Viene descritto e illustrato come creare una trasformazione del flusso di dati con output sincroni tramite il componente script. Questo tipo di trasformazione modifica righe di dati sul posto non appena attraversano il componente.  
  
 [Creazione di una trasformazione asincrona con il componente script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 Viene descritto e illustrato come creare una trasformazione del flusso di dati con output asincroni tramite il componente script. Questo tipo di trasformazione deve leggere tutte le righe di dati prima di poter aggiungere ulteriori informazioni, ad esempio aggregazioni calcolate, ai dati che attraversano il componente.  
  
 [Creazione di una destinazione con il componente script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 Viene descritto e illustrato come creare una destinazione del flusso di dati tramite il componente script.  
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Sviluppo di tipi specifici di componenti del flusso di dati](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
