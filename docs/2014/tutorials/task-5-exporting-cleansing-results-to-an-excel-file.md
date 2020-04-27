---
title: 'Attività 5: esportazione dei risultati della pulizia in un file di Excel | Microsoft Docs'
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489120"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Attività 5: Esportazione dei risultati della pulizia in un file di Excel
  In questa attività vengono esportati i risultati dell'attività di pulizia in un file di Excel. Per ulteriori informazioni, vedere l'argomento relativo alla [fase di esportazione](https://msdn.microsoft.com/library/hh213061.aspx#Export) .  
  
1.  Nel riquadro di destra selezionare **Excel** per il **tipo di destinazione**.  
  
2.  Fare clic su **Sfoglia**, specificare il nome del file di output come **cleaned Supplier List. xls**, quindi fare clic su **Apri**.  
  
3.  Selezionare **solo i dati** per il formato di **output** per esportare solo i dati puliti. La seconda opzione, **dati e informazioni pulizia**, consente di esportare i dettagli delle attività di pulizia insieme ai dati puliti. L'opzione **standardizzazione formato** consente di applicare i formati di output definiti in un dominio ai valori di tale dominio. Non è stato definito un formato di output in un dominio nell'esercitazione.  
  
     ![Pagina Esporta risultati pulizia](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "Pagina Esporta risultati pulizia")  
  
4.  Fare clic su **Esporta** per esportare i dati. Non fare ancora clic su **fine** .  
  
5.  Fare clic su **Chiudi** nella finestra di dialogo **esportazione** .  
  
6.  Fare clic su **fine** per completare l'attività. Se si dimentica di esportare i risultati prima di fare clic su **fine**, fare clic su **Apri progetto Data Quality** nella pagina principale del **client DQS**, selezionare **Pulisci fornitore** dall'elenco di progetti e fare clic su **Avanti** nella parte inferiore della schermata per tornare alla fase di **esportazione** del processo di pulizia. È anche possibile passare alla scheda **Gestisci e visualizza risultati** facendo clic sul pulsante **indietro** .  
  
7.  Aprire **cleaned Supplier List. xls** ed eseguire le operazioni seguenti:  
  
    1.  Verificare che non esistano indirizzi di posta elettronica che terminano con adventure-work.com (senza carattere ') cercando adventure-work.com nel foglio di.  
  
    2.  Vedere che non è presente alcun valore di **USA** nella colonna **Country** .  
  
    3.  Cercare **Los Angeles** e verificare che lo **stato** sia impostato su **CA**.  
  
    4.  Verificare che non siano presenti termini **Co.**, **Corp.** e **Inc.**  
  
    5.  Eliminare la colonna **convalida indirizzo** dal foglio di calcolo e salvare il file di Excel. Questa colonna aggiuntiva corrisponde al dominio composito Address Validation.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 6: Importazione di valori dal progetto Cleanse Supplier List](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
