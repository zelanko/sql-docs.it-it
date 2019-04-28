---
title: Aggiungere funzionalità di Business Intelligence a una dimensione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], dimension intelligence
- dimensions [Analysis Services], Business Intelligence enhancements
- dimension intelligence [Analysis Services]
- Type property
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bee662934a8c63393da3fdf1f6c64b3e9def579
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726931"
---
# <a name="add-dimension-intelligence-to-a-dimension"></a>Aggiungere funzionalità di Business Intelligence per le dimensioni a una dimensione
  L'aggiunta delle funzionalità avanzate di Business Intelligence per le dimensioni a un cubo o una dimensione consente di specificare un tipo di attività standard per una dimensione. Queste funzionalità avanzate specificano inoltre i tipi corrispondenti per gli attributi dimensione. Queste specifiche del tipo possono essere utilizzate dalle applicazioni client per l'analisi dei dati.  
  
 Per aggiungere funzionalità di Business Intelligence per le dimensioni, usare Configurazione guidata funzionalità di Business Intelligence e quindi selezionare l'opzione **Definizione funzionalità di Business Intelligence per le dimensioni** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi relativi alla selezione di una dimensione alla quale si desidera applicare la funzionalità di Business Intelligence per le dimensioni e all'identificazione degli attributi per la dimensione selezionata.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Funzionalità di Business Intelligence per le dimensioni** della procedura guidata specificare la dimensione alla quale si desidera applicare la funzionalità di Business Intelligence per le dimensioni. L'aggiunta della funzionalità avanzata di Business Intelligence per le dimensioni alla dimensione selezionata implica modifiche alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
> [!NOTE]  
>  Se come dimensione si seleziona **Conto** , verrà specificata la funzionalità di Business Intelligence per la contabilità per la dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="specifying-dimension-attributes"></a>Definizione degli attributi dimensione  
 Nel **definiscono funzionalità di Business Intelligence** nella pagina **tipo di dimensione** dall'elenco di selezione effettuata imposta la dimensione `Type` proprietà. L'impostazione della proprietà `Type` fornisce informazioni sul contenuto di una dimensione a server e applicazioni client. Alcune impostazioni forniscono solo indicazioni per le applicazioni client e pertanto queste impostazioni sono facoltative. Altre impostazioni, ad esempio Conti o Ora, determinano funzionalità specifiche e possono essere obbligatorie per l'implementazione di particolari funzionalità avanzate di Business Intelligence. Ad esempio, SQL Server Management Studio utilizza il tipo di dimensione per identificare una dimensione di tipo Valuta e impostare le regole di conversione appropriate per la valuta. L'impostazione predefinita per **Tipo dimensione** è **Regolare**, ovvero non viene usato alcun contenuto specifico della dimensione.  
  
 Dopo aver selezionato il tipo di dimensione, in **Attributi dimensione**nella colonna **Includi** selezionare la casella di controllo accanto a ogni tipo di attributo standard per il quale esiste un attributo corrispondente nella dimensione. Nella colonna **Attributo dimensione** espandere l'elenco a discesa e selezionare l'attributo nella dimensione corrispondente al tipo di attributo selezionato. La selezione dell'attributo dall'elenco comporta l'impostazione della proprietà `Type` degli attributi.  
  
 Si supponga, ad esempio, di voler aggiungere la funzionalità di Business Intelligence per le dimensioni a una dimensione di tipo Conti. In **Tipo dimensione**selezionare **Conti**. Se la dimensione dispone degli attributi **Account Type** e **Account Description** , nella colonna **Includi** selezionare la casella di controllo per i tipi di conto **Account Name** e **Account Type** . Nella colonna **Attributo dimensione** associare questi tipi di conto rispettivamente agli attributi **Account Description** e **Account Type** nella dimensione.  
  
## <a name="see-also"></a>Vedere anche  
 [Definire calcoli delle funzionalità di Business Intelligence per le gerarchie temporali mediante la Configurazione guidata funzionalità di Business Intelligence](define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  
