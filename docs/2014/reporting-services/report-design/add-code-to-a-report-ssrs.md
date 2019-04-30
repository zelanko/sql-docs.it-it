---
title: Aggiungere codice a un report (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f117c8ba2bc933747c725662100cf438dcd67a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185945"
---
# <a name="add-code-to-a-report-ssrs"></a>Aggiungere codice a un report (SSRS)
  In qualsiasi espressione, è possibile chiamare un codice personalizzato. Il codice può essere fornito nei due modi seguenti:  
  
-   Codice scritto in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] direttamente incorporato nel report. Se il codice si riferisce a un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] che non è <xref:System.Math> o <xref:System.Convert>, è necessario aggiungere il riferimento al report. Per altre informazioni, vedere [Aggiungere un riferimento a un assembly in un report &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md). Per altre informazioni sugli altri riferimenti che è possibile creare a partire dal codice, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
-   Fornire un assembly di codice personalizzato mediante [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. L'eventuale assembly personalizzato dovrà essere installato sia nel computer in cui viene creato il report sia nel server di report in cui viene visualizzato il report. Per altre informazioni, vedere [Utilizzo di assembly personalizzati con i report](../custom-assemblies/using-custom-assemblies-with-reports.md).  
  
### <a name="to-add-embedded-code-to-a-report"></a>Per aggiungere codice incorporato a un report  
  
1.  Nella visualizzazione **Progettazione** fare clic con il pulsante destro del mouse nell'area di progettazione all'esterno del bordo del report e scegliere **Proprietà report**.  
  
2.  Fare clic su **Codice**.  
  
3.  Digitare il codice in **Codice personalizzato**. Eventuali errori nel codice genereranno avvisi durante l'esecuzione del report. L'esempio seguente crea una funzione personalizzata denominata `ChangeWord` che sostituisce la parola "`Bike`" con "`Bicycle`".  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  Nell'esempio seguente verrà illustrato come passare un campo del set di dati denominato Category a questa funzione in un'espressione:  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     Se si aggiunge questa espressione a una cella della tabella in cui sono visualizzati i valori della categoria, ogni qualvolta la parola "Bike" è nel campo del set di dati per la riga, nella cella della tabella viene visualizzata invece la parola "Bicycle".  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Proprietà report, Codice](../report-properties-dialog-box-code.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
