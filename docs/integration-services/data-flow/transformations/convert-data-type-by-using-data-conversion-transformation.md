---
title: Convertire un tipo di dati tramite la trasformazione Conversione dati | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 283c033a7c34342c6460ff9acca96e976d1f35a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112690"
---
# <a name="convert-data-type-by-using-data-conversion-transformation"></a>Convertire un tipo di dati tramite la trasformazione Conversione dati

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una trasformazione Conversione dati solo se il pacchetto include già almeno un'attività Flusso di dati e un'origine.  
  
### <a name="to-convert-data-to-a-different-data-type"></a>Per convertire i dati in un tipo di dati diverso  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**, trascinare la trasformazione Conversione dati sull'area di progettazione.  
  
4.  Connettere la trasformazione Conversione dati al flusso di dati trascinando un connettore dall'origine o dalla trasformazione precedente alla trasformazione Conversione dati.  
  
5.  Fare doppio clic sulla trasformazione Conversione dati.  
  
6.  Nella tabella **Colonne di input disponibili** della finestra di dialogo **Editor trasformazione Conversione dati** selezionare le caselle di controllo accanto alle colonne di cui si vuole convertire il tipo di dati.  
  
    > [!NOTE]  
    >  È possibile applicare più conversioni di dati a una singola colonna di input.  
  
7.  Facoltativamente, modificare i valori predefiniti nella colonna **Alias di output** .  
  
8.  Nell'elenco **Tipo di dati** selezionare il nuovo tipo di dati per la colonna. Il tipo di dati predefinito è quello della colonna di input.  
  
9. A seconda del tipo di dati selezionato, aggiornare facoltativamente i valori nelle colonne **Lunghezza**, **Precisione**, **Scala**e **Tabella codici** .  
  
10. Per configurare l'output degli errori, fare clic su **Configura output errori**. Per altre informazioni, vedere [Debug di un flusso di dati](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Fare clic su **OK**.  
  
12. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)  
  
  
