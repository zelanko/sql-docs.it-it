---
title: Finestra di dialogo Proprietà set di dati, campi | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 133d905958f0613d9b7ecf2d28c439c15a59eedb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109398"
---
# <a name="dataset-properties-dialog-box-fields"></a>Finestra di dialogo Proprietà set di dati, Campi
  Selezionare **Campi** nella finestra di dialogo **Proprietà set di dati** per modificare la raccolta di campi per il set di dati del report. L'elenco dei campi viene generato automaticamente, tuttavia è possibile usare la scheda **Campi** per aggiungere, modificare ed eliminare campi di query e calcolati.  
  
## <a name="options"></a>Opzioni  
 **Aggiungi**  
 Consente di aggiungere un nuovo campo di query o campo calcolato al set di dati.  
  
 **Elimina**  
 Consente di eliminare il campo selezionato dal set di dati.  
  
 **Nome del campo**  
 Consente di digitare un nome per il campo. Il campo deve essere univoco nel set di dati. Per ogni campo esistente nella query del set di dati, il nome viene prepopolato.  
  
 **Origine campo**  
 Immettere un valore per il campo.  
  
 Per un campo calcolato, l'origine del campo deve essere il nome di un campo esistente recuperato dalla query del set di dati o da un'espressione creata. Ad esempio, per creare un campo che rappresenta 10 volte il valore nel campo Sales della query, utilizzare l'espressione `=10 * Fields!Sales.Value`.  
  
 Per un campo query, l'origine del campo deve essere il nome di un campo esistente recuperato dalla query del set di dati.  
  
 **Espressione (fx)**  
 Consente di aggiungere o modificare un'espressione per il campo calcolato. Questo pulsante viene visualizzato solo quando si fa clic su **Aggiungi** e si seleziona **Campo calcolato**.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
