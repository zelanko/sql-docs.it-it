---
title: 'Attività 5: Esportazione dei risultati in un File di Excel di pulizia | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489120"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Attività 5: Esportazione dei risultati della pulizia in un file di Excel
  In questa attività vengono esportati i risultati dell'attività di pulizia in un file di Excel. Visualizzare [fase di esportazione](https://msdn.microsoft.com/library/hh213061.aspx#Export) per altre informazioni.  
  
1.  Nel riquadro di destra, selezionare **Excel** per il **tipo di destinazione**.  
  
2.  Fare clic su **esplorare**, specificare il nome di file di output come **Cleansed Supplier List. xls**, quindi fare clic su **Open**.  
  
3.  Selezionare **Data Only** per il **Output** formato esportare solo i dati puliti. La seconda opzione, **dei dati e informazioni pulizia**, consente di esportare i dettagli dell'attività pulizia insieme ai dati puliti. Il **standardizzare formato** opzione consente di applicare qualsiasi formati di output definiti in un dominio ai valori di tale dominio. Non è stato definito un formato di output in un dominio nell'esercitazione.  
  
     ![Pagina dei risultati di esportazione Cleansing](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "esportazione pulizia pagina risultati")  
  
4.  Fare clic su **esportare** per esportare i dati. Non fare clic **fine** ancora.  
  
5.  Fare clic su **Close** nel **esportazione** nella finestra di dialogo.  
  
6.  Fare clic su **fine** per completare l'attività. Se si dimentica di esportare i risultati prima di fare clic **Finish**, fare clic su **Apri progetto Data Quality** nella pagina principale del **Client DQS**, selezionare **Cleanse Supplier Elenco** dall'elenco dei progetti, fare clic su **successivo** nella parte inferiore della schermata per ottenere il **Esporta** fase del processo di pulizia. È anche possibile passare a **Gestisci e Visualizza risultati** scheda, fare clic su **nuovamente** pulsante.  
  
7.  Aprire il **Cleansed Supplier List. xls** eseguire le operazioni seguenti:  
  
    1.  Assicurarsi che non sono presenti indirizzi di posta elettronica che terminano con Adventure-Work.com (senza del carattere ') cercando Adventure-Work.com nel foglio di lavoro.  
  
    2.  Riscontrerebbe che è presente alcun **Stati Uniti** valore nel **paese** colonna.  
  
    3.  Cercare **Los Angeles** e verificare che il **stato** è impostata su **CA**.  
  
    4.  Verificare che vi sia alcun termine **co**, **corp**, e **Inc.** .  
  
    5.  Eliminare il **Address Validation** colonna dal foglio di calcolo e salvare il file di excel. Questa colonna aggiuntiva corrisponde al dominio composito Address Validation.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 6: Importazione di valori dal progetto Cleanse Supplier List](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
