---
title: 'Lezione 2: Definizione delle informazioni di connessione (Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: da47a0fd587d48dd9d932504d6a5cd45d0d54664
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294699"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lezione 2: Definizione delle informazioni di connessione (Reporting Services)
Dopo aver aggiunto un report impaginato [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] al progetto dell'esercitazione nella Lezione 1, è necessario definire un'*origine dati*, vale a dire informazioni di connessione usate dal report per accedere ai dati da un database relazionale, multidimensionale o da un'altra risorsa.  
  
In questa lezione verrà usato come origine dati il database di esempio [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]. Durante l'esercitazione si presuppone che il database si trovi nell'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] installata nel computer locale.  
  
### <a name="to-set-up-a-connection"></a>Per impostare una connessione  
  
1.  Nel riquadro **Dati report** , fare clic su **Nuova** , quindi su **Data Source**.  
Se il riquadro **Dati report** non è visualizzato, scegliere **Dati report** dal menu **Visualizza**.  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  Nella casella **Nome**digitare *AdventureWorks2014*.  
  
3.  Accertarsi che sia selezionata l'opzione **Connessione incorporata** .  
  
4.  In **Tipo**selezionare **Microsoft SQL Server**.  
  
5.  In **Stringa di connessione**digitare quanto segue:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     Per questa stringa di connessione si presuppone che [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], il server di report e il database [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] siano installati nel computer locale e che si disponga dell'autorizzazione per l'accesso al database [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . Se il database AdventureWorks2014 non è presente nel computer locale, modificare la stringa di connessione e sostituire *localhost* con il nome dell'istanza del server di database.
  
     >[!NOTE]  
    >Se si utilizza [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services oppure un'istanza denominata, è necessario includere nella stringa di connessione le informazioni sull'istanza:  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >Per altre informazioni sulle stringhe di connessione, vedere: [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
     
  
6.  Fare clic su **Credenziali** nel riquadro sinistro e selezionare **Usa autenticazione di Windows (sicurezza integrata)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] L'origine dati **AdventureWorks2014** verrà aggiunta al riquadro **Dati report** .  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>Attività successiva  
È stata definita correttamente una connessione al database di esempio [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . Verrà successivamente creato il report. Vedere [Lezione 3: Definizione di un set di dati per il report tabella &#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
[Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  

