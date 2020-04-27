---
title: Aggiunta dell'attività Flusso di dati a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b72669c44e3cf95076473c207c50cbcabf54b1ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62836914"
---
# <a name="adding-the-data-flow-task-programmatically"></a>Aggiunta dell'attività Flusso di dati a livello di programmazione
  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è inclusa l'attività Flusso di dati, rappresentata dallo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> del modello a oggetti. Flusso di dati è un'attività speciale, a elevate prestazioni, dedicata alla trasformazione e allo spostamento dei dati durante l'esecuzione del pacchetto. Analogamente ad altre attività, Flusso di dati è inclusa nell'oggetto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> e dal punto di vista del motore di run-time è solo un'altra attività del pacchetto. Tuttavia, il flusso di dati contiene oggetti aggiuntivi denominati componenti del flusso di dati. Si tratta dei componenti che consentono lo spostamento dei dati da un'origine a una destinazione, a volte tramite una trasformazione. Tali componenti definiscono sia la direzione dello spostamento che la modalità di trasformazione dei dati. La configurazione dell'attività Flusso di dati implica l'aggiunta di componenti e quindi la relativa connessione per stabilire il flusso dei dati e ottenere la trasformazione desiderata.  
  
 Un'attività Flusso di dati include tre tipi di componenti: **Origini flusso di dati**, **Trasformazioni flusso di dati** e **Destinazioni flusso di dati**, visualizzati in questo ordine nella casella degli strumenti di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Questi tipi vengono anche definiti più semplicemente come origini, trasformazioni o destinazioni. Come implicano i nomi, i dati vengono spostati da un'origine a una trasformazione e quindi a una destinazione. Si tratta di una descrizione semplicistica del flusso di dati per illustrare il concetto, ma l'attività Flusso di dati è sufficientemente flessibile e potente da gestire più origini e da connettere molte trasformazioni che inviano l'output a molte destinazioni.  
  
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
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedi anche  
 [Individuazione dei componenti del flusso di dati a livello di programmazione](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
