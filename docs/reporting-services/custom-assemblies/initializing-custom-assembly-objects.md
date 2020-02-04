---
title: Inizializzazione di oggetti assembly personalizzati | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8bef8bcf36629b0cb31afef31f4d9a199313f015
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193952"
---
# <a name="initializing-custom-assembly-objects"></a>Inizializzazione di oggetti assembly personalizzati
  In alcuni casi, potrebbe essere necessario inizializzare valori di proprietà e campi nelle classi di assembly personalizzate quando si crea un'istanza di tali classi. In genere, è necessario inizializzare le classi personalizzate con i valori disponibili nelle raccolte di oggetti globali del report. A tale scopo, è possibile eseguire l'override del metodo **OnInit** dell'oggetto **Code** di un report. Per accedere al metodo **OnInit**, usare l'elemento **Code** della definizione del report. Per l'inizializzazione di valori di campo o proprietà delle classi in un assembly personalizzato da usare in un report sono disponibili due tecniche. È possibile dichiarare e creare una nuova istanza della classe tramite **OnInit** oppure è possibile chiamare un metodo disponibile pubblicamente tramite **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Raccolte di oggetti globali e inizializzazione  
 Per l'inizializzazione delle variabili delle classi personalizzate sono disponibili diverse raccolte. È possibile usare le raccolte **Globals** e **User**. Le raccolte **Parameters**, **Fields** e **ReportItems** non sono disponibili nel ciclo di vita del report durante il quale viene richiamato il metodo **OnInit**. Per usare le raccolte condivise **Globals** o **User**, è necessario includere il riferimento all'oggetto **Report**. Ad esempio, per inizializzare la classe personalizzata in base alla lingua corrente dell'utente che accede al report, l'elemento **Code** può essere simile al seguente:  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Per inizializzare valori di proprietà e campi di una classe come illustrato in precedenza, è possibile dichiarare la classe e creare una nuova istanza chiamando un costruttore sottoposto a override.  
  
 In alternativa, per inizializzare i valori di proprietà e campi delle classi negli assembly personalizzati, è possibile chiamare un metodo disponibile pubblicamente definito dal metodo **OnInit**. È innanzitutto necessario aggiungere un nome di istanza per la classe nel file di definizione del report. Dopo avere aggiunto il nome di istanza e il riferimento all'assembly appropriati, è possibile chiamare il metodo di inizializzazione per inizializzare i valori di proprietà e campi per la classe. Il metodo **OnInit** può essere simile al seguente:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Per altre informazioni sull'aggiunta di un riferimento all'assembly e di un nome di istanza per la classe personalizzata, vedere [Aggiungere un riferimento a un assembly in un report &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Per altre informazioni sulle raccolte di oggetti globali, vedere [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di assembly personalizzati con i report](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
