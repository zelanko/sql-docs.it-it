---
title: Aggiornamento della versione di un componente del flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- PerformUpgrade method
- custom data flow components [Integration Services], upgrading version
- data flow components [Integration Services], upgrading version
- upgrading data flow components [Integration Services]
ms.assetid: c2a298c6-01b3-4ad1-884d-6108165eb56e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 33ea6f845c323a858d1bd89318f2b8e07b734edd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896097"
---
# <a name="upgrading-the-version-of-a-data-flow-component"></a>Aggiornamento della versione di un componente del flusso di dati
  I pacchetti creati con una versione precedente del componente possono contenere metadati non più validi, ad esempio proprietà personalizzate il cui utilizzo è stato modificato nelle versioni più recenti del componente. È possibile eseguire l'override del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> della classe di base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> per aggiornare i metadati salvati in precedenza in pacchetti meno recenti in base alle proprietà correnti del componente.  
  
> [!NOTE]  
>  Quando si ricompila un componente personalizzato per una nuova versione di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], non è necessario modificare il valore della proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> se le proprietà del componente non sono state modificate.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente contiene codice della versione 2.0 di un componente del flusso di dati fittizio. Il nuovo numero di versione è definito nella proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> di <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Il componente include una proprietà che definisce la modalità di gestione dei valori numerici che superano una determinata soglia. Nella versione 1.0 del componente fittizio questa proprietà è denominata `RaiseErrorOnInvalidValue` e accetta il valore booleano true o false. Nella versione 2.0 del componente fittizio la proprietà è stata rinominata in `InvalidValueHandling` e accetta uno dei quattro valori possibili di un enumeratore personalizzato.  
  
 Il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> sottoposto a override nell'esempio effettua le azioni seguenti:  
  
-   Ottiene la versione corrente del componente.  
  
-   Ottiene il valore della proprietà personalizzata precedente.  
  
-   Rimuove la proprietà precedente dalla raccolta di proprietà personalizzate.  
  
-   Imposta il valore della nuova proprietà personalizzata in base al valore di quella precedente, se possibile.  
  
-   Imposta i metadati della versione sulla versione corrente del componente.  
  
> [!NOTE]  
>  Il motore flusso di dati passa il proprio numero di versione al metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> nel parametro *pipelineVersion*. Questo parametro non è utile nella versione 1.0 di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], ma può diventarlo nelle versioni successive.  
  
 Nel codice di esempio vengono utilizzati solo i due valori di enumerazione che possono essere mappati direttamente ai valori booleani precedenti per la proprietà personalizzata. Gli utenti possono selezionare gli altri valori di enumerazione disponibili tramite l'interfaccia utente personalizzata del componente, nell'editor avanzato o a livello di codice. Per informazioni sulla visualizzazione di valori di enumerazione per una proprietà personalizzata nell'Editor avanzato, vedere "Creazione di proprietà personalizzate" in [Metodi della fase di progettazione di un componente flusso di dati](design-time-methods-of-a-data-flow-component.md).  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(ComponentType:=ComponentType.Transform, CurrentVersion:=2)> _  
Public Class PerformUpgrade  
  Inherits PipelineComponent  
  
  ' Define the set of possible values for the new custom property.  
  Private Enum InvalidValueHandling  
    Ignore  
    FireInformation  
    FireWarning  
    FireError  
  End Enum  
  
  Public Overloads Overrides Sub PerformUpgrade(ByVal pipelineVersion As Integer)  
  
    ' Obtain the current component version from the attribute.  
    Dim componentAttribute As DtsPipelineComponentAttribute = _  
      CType(Attribute.GetCustomAttribute(Me.GetType, _  
      GetType(DtsPipelineComponentAttribute), False), _  
      DtsPipelineComponentAttribute)  
    Dim currentVersion As Integer = componentAttribute.CurrentVersion  
  
    ' If the component version saved in the package is less than  
    '  the current version, Version 2, perform the upgrade.  
    If ComponentMetaData.Version < currentVersion Then  
  
      ' Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
      ' and then remove the property from the custom property collection.  
      Dim oldValue As Boolean = False  
      Try  
        Dim oldProperty As IDTSCustomProperty100 = _  
          ComponentMetaData.CustomPropertyCollection("RaiseErrorOnInvalidValue")  
        oldValue = CType(oldProperty.Value, Boolean)  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue")  
      Catch ex As Exception  
        ' If the old custom property is not available, ignore the error.  
      End Try  
  
      ' Set the value of the new custom property, InvalidValueHandling,  
      '  by using the appropriate enumeration value.  
      Dim newProperty As IDTSCustomProperty100 = _  
        ComponentMetaData.CustomPropertyCollection("InvalidValueHandling")  
      If oldValue = True Then  
        newProperty.Value = InvalidValueHandling.FireError  
      Else  
        newProperty.Value = InvalidValueHandling.Ignore  
      End If  
  
    End If  
  
    ' Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
[DtsPipelineComponent(ComponentType = ComponentType.Transform, CurrentVersion = 2)]  
public class PerformUpgradeCS :  
  PipelineComponent  
  
  // Define the set of possible values for the new custom property.  
{  
  private enum InvalidValueHandling  
  {  
    Ignore,  
    FireInformation,  
    FireWarning,  
    FireError  
  };  
  
  public override void PerformUpgrade(int pipelineVersion)  
  {  
  
    // Obtain the current component version from the attribute.  
    DtsPipelineComponentAttribute componentAttribute =   
      (DtsPipelineComponentAttribute)Attribute.GetCustomAttribute(this.GetType(), typeof(DtsPipelineComponentAttribute), false);  
    int currentVersion = componentAttribute.CurrentVersion;  
  
    // If the component version saved in the package is less than  
    //  the current version, Version 2, perform the upgrade.  
    if (ComponentMetaData.Version < currentVersion)  
  
    // Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
    // and then remove the property from the custom property collection.  
    {  
      bool oldValue = false;  
      try  
      {  
        IDTSCustomProperty100 oldProperty =   
          ComponentMetaData.CustomPropertyCollection["RaiseErrorOnInvalidValue"];  
        oldValue = (bool)oldProperty.Value;  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue");  
      }  
      catch (Exception ex)  
      {  
        // If the old custom property is not available, ignore the error.  
      }  
  
      // Set the value of the new custom property, InvalidValueHandling,  
      //  by using the appropriate enumeration value.  
      IDTSCustomProperty100 newProperty =   
         ComponentMetaData.CustomPropertyCollection["InvalidValueHandling"];  
      if (oldValue == true)  
      {  
        newProperty.Value = InvalidValueHandling.FireError;  
      }  
      else  
      {  
        newProperty.Value = InvalidValueHandling.Ignore;  
      }  
  
    }  
  
    // Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion;  
  
  }  
  
}  
```  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
