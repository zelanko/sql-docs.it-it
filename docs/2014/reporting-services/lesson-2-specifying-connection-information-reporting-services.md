---
title: 'Lezione 2: Definizione delle informazioni di connessione (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cd0c7e3bc9ece2a6eafa9de1623bfa2b641e5e64
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59955577"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lezione 2: Definizione delle informazioni di connessione (Reporting Services)
  Dopo aver aggiunto un report al progetto Tutorial, è necessario definire un' *origine dati*, vale a dire informazioni di connessione usate dal report per accedere ai dati da un database relazionale, da un database multidimensionale o da un'altra risorsa.  
  
 In questa lezione come origine dati verrà utilizzato il database di esempio [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. L'esercitazione presuppone che il database si trovi in un'istanza predefinita del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] installata nel computer locale.  
  
### <a name="to-set-up-a-connection"></a>Per impostare una connessione  
  
1.  Nel **i dati del Report** riquadro, fare clic su **New** e quindi fare clic su **Zdroj dat...** .  
  
    > [!NOTE]  
    >  Se il riquadro **Dati report** non è visualizzato, scegliere **Dati report** dal menu **Visualizza**.  
  
2.  In **Nome**digitare [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)].  
  
3.  Accertarsi che sia selezionata l'opzione **Connessione incorporata** .  
  
4.  In **Tipo**selezionare **Microsoft SQL Server**.  
  
5.  In **Stringa di connessione**digitare quanto segue:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
     Per questa stringa di connessione si presuppone che [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], il server di report e il database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] siano installati nel computer locale e che si disponga dell'autorizzazione per l'accesso al database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  
  
    > [!NOTE]  
    >  Se si utilizza [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services oppure un'istanza denominata, è necessario includere nella stringa di connessione le informazioni sull'istanza:  
    >   
    >  `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2012`  
    >   
    >  Per altre informazioni sulle stringhe di connessione, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](data-connections-data-sources-and-connection-strings-in-reporting-services.md) e [finestra di dialogo Proprietà origine dati, generale](data-source-properties-dialog-box-general.md).  
  
6.  Fare clic su **Credenziali** nel riquadro sinistro e selezionare **Usa autenticazione di Windows (sicurezza integrata)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] zdroj dat [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] viene aggiunto per il **i dati del Report** riquadro.  
  
## <a name="next-task"></a>Attività successiva  
 È stata definita correttamente una connessione al database di esempio [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Verrà successivamente creato il report. Vedere [Lezione 3: Definizione di un set di dati per il report tabella &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
