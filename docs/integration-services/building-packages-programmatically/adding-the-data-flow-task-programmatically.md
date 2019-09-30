---
title: Aggiunta dell'attività Flusso di dati a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: db9545df35823161dbe6fa64673cac1361c3d34b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294917"
---
# <a name="adding-the-data-flow-task-programmatically"></a>Aggiunta dell'attività Flusso di dati a livello di programmazione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è inclusa l'attività Flusso di dati, rappresentata dallo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> del modello a oggetti. Flusso di dati è un'attività speciale, a elevate prestazioni, dedicata alla trasformazione e allo spostamento dei dati durante l'esecuzione del pacchetto. Analogamente ad altre attività, Flusso di dati è inclusa nell'oggetto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> e dal punto di vista del motore di run-time è solo un'altra attività del pacchetto. Tuttavia, il flusso di dati contiene oggetti aggiuntivi denominati componenti del flusso di dati. Si tratta dei componenti che consentono lo spostamento dei dati da un'origine a una destinazione, a volte tramite una trasformazione. Tali componenti definiscono sia la direzione dello spostamento che la modalità di trasformazione dei dati. La configurazione dell'attività Flusso di dati implica l'aggiunta di componenti e quindi la relativa connessione per stabilire il flusso dei dati e ottenere la trasformazione desiderata.  
  
 Esistono tre tipi di componenti all'interno di un'attività Flusso di dati: **Origini flusso di dati**, **Trasformazioni flusso di dati** e **Destinazioni flusso di dati**, visualizzati in questo ordine nella casella degli strumenti di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Questi tipi vengono anche definiti più semplicemente come origini, trasformazioni o destinazioni. Come implicano i nomi, i dati vengono spostati da un'origine a una trasformazione e quindi a una destinazione. Si tratta di una descrizione semplicistica del flusso di dati per illustrare il concetto, ma l'attività Flusso di dati è sufficientemente flessibile e potente da gestire più origini e da connettere molte trasformazioni che inviano l'output a molte destinazioni.  
  
 L'attività Flusso di dati viene aggiunta in un pacchetto allo stesso modo delle altre attività. Una volta aggiunta, l'attività viene configurata con l'aggiunta, la configurazione e la connessione dei relativi componenti.  
  
## <a name="sample"></a>Esempio  
 Nell'esempio di codice seguente viene illustrato come aggiungere un'attività Flusso di dati in un pacchetto. L'esempio richiede un riferimento agli assembly Microsoft.SqlServer.PipelineHost, Microsoft.SqlServer.DTSPipelineWrap e Microsoft.SqlServer.ManagedDTS.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sull'[aggiornamento di EzAPI per SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223) sul sito Web blogs.msdn.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Individuazione dei componenti del flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
