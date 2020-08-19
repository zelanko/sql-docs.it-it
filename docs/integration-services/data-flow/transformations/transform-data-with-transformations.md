---
description: Trasformazione di dati con le trasformazioni
title: Trasformare dati con le trasformazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2d9422574f80febefc6458b389f04b4b1625b22c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425653"
---
# <a name="transform-data-with-transformations"></a>Trasformazione di dati con le trasformazioni

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sono disponibili tre tipi di componenti flusso di dati: origini, trasformazioni e destinazioni.  
  
 Nella figura seguente viene illustrato un semplice flusso di dati con un'origine, due trasformazioni e una destinazione.  
  
 ![Flusso di dati](../../../integration-services/data-flow/media/mw-dts-08.gif "Flusso di dati")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Le trasformazioni offrono le funzionalità seguenti:  
  
-   Divisione, copia e unione dei set di righe ed esecuzione di operazioni di ricerca.  
  
-   Aggiornamento dei valori delle colonne e creazione di nuove colonne tramite l'applicazione di trasformazioni, quale quella per la conversione dei caratteri da minuscolo a maiuscolo.  
  
-   Esecuzione di operazioni di Business Intelligence quali la pulitura dei dati, il text mining e l'esecuzione di query di stima basate su algoritmi di data mining.  
  
-   Creazione di nuovi set di righe costituiti da valori ordinati o di aggregazione, dati campione o trasformati tramite Pivot o UnPivot.  
  
-   Esecuzione di attività quali quelle per l'esportazione e l'importazione di dati, la generazione di informazioni di controllo e l'utilizzo di dimensioni a modifica lenta.  
  
 Per altre informazioni, vedere [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
 È inoltre possibile creare trasformazioni personalizzate. Per altre informazioni, vedere [Sviluppo di un componente del flusso di dati personalizzato](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e [Sviluppo di tipi specifici di componenti del flusso di dati](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md).  
  
 Dopo l'aggiunta della trasformazione alla finestra di progettazione del flusso di dati, ma prima della sua configurazione, è possibile connettere la trasformazione al flusso di dati connettendo l'output di un'altra trasformazione o di un'altra origine nel flusso di dati all'input della nuova trasformazione. Il connettore tra due componenti del flusso di dati è detto percorso. Per altre informazioni sulla connessione di componenti e l'uso dei percorsi, vedere [Connessione di componenti con i percorsi](https://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8).  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>Per aggiungere una trasformazione a un flusso di dati  
  
-   [Aggiunta o eliminazione di un componente in un flusso di dati](../../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>Per connettere una trasformazione a un flusso di dati  
  
-   [Connessione di componenti in un flusso di dati](../../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>Per impostare le proprietà di una trasformazione  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Connessione di componenti con i percorsi](https://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8)   
 [Gestione degli errori nei dati](../../../integration-services/data-flow/error-handling-in-data.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)  
  
  
