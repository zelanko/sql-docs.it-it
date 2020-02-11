---
title: Editor trasformazione Esportazione colonna (pagina colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0d5e37211471285e971ba29bc3419e759b0c7af7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059006"
---
# <a name="export-column-transformation-editor-columns-page"></a>Editor trasformazione Esportazione colonna (pagina Colonne)
  Utilizzare la pagina **Colonne** della finestra di dialogo **Editor trasformazione Esportazione colonna** per specificare le colonne nel flusso di dati da estrarre in file. È possibile indicare se la trasformazione Esporta colonna deve accodare i dati a un file oppure sovrascrivere un file esistente.  
  
 Per ulteriori informazioni sulla trasformazione Esportazione colonna, vedere [Export Column Transformation](data-flow/transformations/export-column-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Estrai colonna**  
 Consente di eseguire una selezione dall'elenco di colonne di input contenenti dati di tipo text o image. In tutte le righe devono essere presenti definizioni per **Colonna estrazione** e **Colonna percorso file**.  
  
 **Colonna percorso file**  
 Consente di eseguire una selezione dall'elenco di colonne di input contenenti nomi e percorsi di file. In tutte le righe devono essere presenti definizioni per **Colonna estrazione** e **Colonna percorso file**.  
  
 **Consenti Accodamento**  
 Consente di indicare se la trasformazione accoderà i dati ai file esistenti. Il valore predefinito è `false`.  
  
 **Forza troncamento**  
 Consente di indicare se la trasformazione eliminerà il contenuto di file esistenti prima di scrivere i dati. Il valore predefinito è `false`.  
  
 **Scrivi BOM**  
 Consente di specificare se scrivere un indicatore ordine byte (BOM) nel file. L'indicatore dell'ordine byte viene scritto solo se i dati hanno tipo di dati `DT_NTEXT` o DT_WSTR e non sono accodati a un file di dati esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor trasformazione Esportazione colonna &#40;pagina output degli errori&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
