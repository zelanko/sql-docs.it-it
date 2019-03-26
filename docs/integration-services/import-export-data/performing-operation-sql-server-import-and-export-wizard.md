---
title: Esecuzione delle operazioni (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.performingoperation.f1
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 05b5e0867d9bbe5ab4ea5e583db40a21aaafe76c
ms.sourcegitcommit: 5683044d87f16200888eda2c2c4dee38ff87793f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58221975"
---
# <a name="performing-operation-sql-server-import-and-export-wizard"></a>Esecuzione delle operazioni (Importazione/Esportazione guidata SQL Server)
Dopo avere esaminato le scelte effettuate nella procedura guidata, fare clic su **Fine** nella pagina **Completare la procedura guidata** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Importazione/Esportazione guidata visualizzerà **Esecuzione dell'operazione**. In questa pagina è possibile visualizzare lo stato di avanzamento e il risultato dell'operazione configurata nelle pagine precedenti. Non è necessario eseguire alcuna operazione in questa pagina.

## <a name="screen-shot---operation-in-progress"></a>Screenshot di operazione in corso 
 L'immagine seguente illustra la pagina **Esecuzione dell'operazione** della procedura guidata mentre l'operazione è ancora in corso.  
  
 ![Pagina Esecuzione dell'operazione dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/performing-operation1.png "Pagina Esecuzione dell'operazione dell'Importazione/Esportazione guidata")  

## <a name="screen-shot---operation-completed"></a>Screenshot di operazione completata 
 L'immagine seguente illustra la pagina **Esecuzione dell'operazione** della procedura guidata al termine dell'operazione. Fare clic su un elemento della colonna **Messaggio** per altre informazioni sul passaggio corrispondente.  
  
 ![Pagina Esecuzione dell'operazione dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/performing-operation2.png "Pagina Esecuzione dell'operazione dell'Importazione/Esportazione guidata")  
  
## <a name="watch-the-progress-of-the-operation"></a>Visualizzare lo stato dell'operazione
 **Azione**  
 Consente di visualizzare ogni passaggio dell'operazione.  
  
 **Stato**  
 Consente di visualizzare l'esito positivo o negativo di ogni passaggio.  
  
 **Messaggio**  
 Visualizza messaggi informativi e di errore relativi al passaggio. Fare clic su un elemento della colonna per altre informazioni sul passaggio corrispondente.

## <a name="interrupt-the-operation-or-save-the-results"></a>Interrompere l'operazione o salvare i risultati
 **Arresta**  
 Consente di interrompere l'operazione, se necessario, usando il pulsante **Arresta** .  
  
 **Report**  
 Consente di visualizzare un report dei risultati, salvarlo in un file, copiarlo negli Appunti o inviarlo tramite posta elettronica.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo che l'operazione configurata è stata eseguita e completata correttamente, l'esecuzione di Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] giunge al termine.  
-   Se si esegue l'operazione immediatamente, è possibile aprire la destinazione selezionata per esaminare i dati copiati dalla procedura guidata.  
-   Se il pacchetto SSIS creato dalla procedura guidata è stato salvato, è possibile aprirlo in SQL Server Data Tools per personalizzarlo e usarlo di nuovo. Per informazioni su come personalizzare il pacchetto salvato ed eseguirlo in un secondo momento, vedere [Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Vedere anche
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


