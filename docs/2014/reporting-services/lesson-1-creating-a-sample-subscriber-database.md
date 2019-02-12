---
title: 'Lezione 1: Creazione di un Database Sottoscrittore di esempio | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5a754f0d81714e3f483ee5abeab1850c61592ab6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039242"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>Lezione 1: Creazione di un Database Sottoscrittore di esempio
  Prima di definire una sottoscrizione guidata dai dati è necessario disporre di un'origine dei dati contenente i dati della sottoscrizione. In questo passaggio vengono illustrate le procedure per la creazione di un piccolo database per archiviare i dati della sottoscrizione utilizzati in questa esercitazione. Successivamente, quando la sottoscrizione viene elaborata, tramite il server di report vengono recuperati i dati e utilizzati per personalizzare l'output di report, le opzioni di recapito e il formato di presentazione del report.  
  
 In questa lezione si presuppone che si usa [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per creare un [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] database.  
  
### <a name="to-create-a-sample-subscriber-database"></a>Per creare un database di esempio del Sottoscrittore  
  
1.  Avviare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e stabilire una connessione a un [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse su Database, quindi scegliere **Nuovo database**.  
  
3.  Nella finestra di dialogo Nuovo Database, in nome del Database, digitare *sottoscrittori*. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Fare clic sul pulsante **Nuova query** sulla barra degli strumenti.  
  
5.  Copiare le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] seguenti nella query vuota:  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
6.  Fare clic su  **Esegui** sulla barra degli strumenti.  
  
7.  Utilizzare un'istruzione SELECT per verificare che siano disponibili tre righe di dati. Esempio: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Passaggi successivi  
 In tal modo sono stati creati i dati di sottoscrizione per la distribuzione dei report e per la variazione dell'output del report per ogni sottoscrittore. Sarà quindi possibile modificare le proprietà dell'origine dei dati del report da distribuire ai sottoscrittori. La modifica delle proprietà dell'origine dei dati viene eseguita per preparare il report per il recapito delle sottoscrizioni guidate dai dati. Inoltre, verrà modificata la progettazione report per includere un parametro che verrà utilizzato dalla sottoscrizione con i dati del sottoscrittore. [Lezione 2: Modifica i dati del Report delle proprietà dell'origine](lesson-2-modifying-the-report-data-source-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Creare un Database](../relational-databases/databases/create-a-database.md)   
 [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
