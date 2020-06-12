---
title: Modificare la proprietà della colonna di colonna di un attributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
ms.openlocfilehash: ad5674f576f7a6cf42b396d3e76db457f068e1ee
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544763"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>Modificare la proprietà KeyColumn di un attributo
  È possibile modificare la proprietà **KeyColumns** di un attributo. Ad esempio, è possibile specificare una chiave composta anziché una chiave semplice come chiave dell'attributo.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Per modificare la proprietà KeyColumns di un attributo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto nel quale si vuole modificare la proprietà **KeyColumns** .  
  
2.  Aprire Progettazione dimensioni effettuando una delle operazioni seguenti:  
  
    -   In **Esplora soluzioni**fare clic con il pulsante destro del mouse sulla dimensione nella cartella **Dimensioni** e quindi scegliere **Apri** o **Progettazione viste**.  
  
         -oppure-  
  
    -   Nella scheda **Struttura cubo** di Progettazione cubi espandere la dimensione del cubo nel riquadro **dimensioni** e fare clic su **modifica \<dimension> **.  
  
3.  Nel riquadro **Attributi** della scheda **Struttura dimensione** fare clic sull'attributo per il quale si vuole modificare la proprietà **KeyColumns** .  
  
4.  Nella finestra **Proprietà** fare clic sul valore della proprietà **KeyColumns** .  
  
5.  Fare clic sul pulsante di ricerca ( **...** ) che viene visualizzato nella cella del valore della casella delle proprietà.  
  
     Verrà visualizzata la finestra di dialogo **Colonne chiave** .  
  
6.  Per rimuovere una colonna chiave esistente, nell'elenco **Colonne chiave** selezionare la colonna e quindi fare clic sul pulsante **\<** .  
  
7.  Per aggiungere una colonna chiave, nell'elenco **Colonne disponibili** selezionare la colonna e quindi fare clic sul pulsante **>** .  
  
    > [!NOTE]  
    >  Se si definiscono più colonne chiave, l'ordine di visualizzazione di tali colonne nell'elenco **Colonne chiave** influisce sull'ordine visualizzato. Ad esempio, l'attributo mese ha due colonne chiave: mese ed anno. Se la colonna anno è visualizzata nell'elenco prima della colonna mese, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordina per anno e quindi per mese. Se la colonna mese appare prima della colonna anno, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordina per mese e quindi per anno.  
  
8.  Per modificare l'ordine delle colonne chiave, selezionare una colonna e quindi fare clic sul pulsante **Su** o **Giù** .  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributo delle dimensioni](dimension-attribute-properties-reference.md)  
  
  
