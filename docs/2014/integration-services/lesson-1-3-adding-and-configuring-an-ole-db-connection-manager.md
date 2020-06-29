---
title: 'Passaggio 3: Aggiunta e configurazione di una gestione connessione OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e7ba771b404ac7d0fad5721fa6056333634e7246
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436078"
---
# <a name="step-3-adding-and-configuring-an-ole-db-connection-manager"></a>Passaggio 3: Aggiunta e configurazione di una gestione connessione OLE DB
  Dopo aver aggiunto una gestione connessione file flat per connettersi all'origine dati, l'operazione successiva consiste nell'aggiunta di una gestione connessione OLE DB per connettersi alla destinazione. Una gestione connessione OLE DB abilita un pacchetto all'estrazione di dati o al caricamento di dati in un'origine dati compatibile con OLE DB. Gestione connessione OLE DB consente di specificare il server, il metodo di autenticazione e il database predefinito per la connessione.  
  
 In questa lezione verrà creata una gestione connessione OLE DB tramite cui viene utilizzata l'autenticazione di Windows per connettersi all'istanza locale di **AdventureWorksDB2012**. Alla gestione connessione OLE DB creata faranno anche riferimento altri componenti che verranno creati più avanti in questa esercitazione, come la trasformazione Ricerca e la destinazione OLE DB.  
  
### <a name="to-add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Per aggiungere e configurare una gestione connessione OLE DB al pacchetto SSIS  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area **Gestioni connessioni** e quindi fare clic su **Nuova connessione OLE DB**.  
  
2.  Nella finestra di dialogo **Configura gestione connessione OLE DB** fare clic su **Nuova**.  
  
3.  Per **Nome server**, immettere **localhost**.  
  
     Quando si specifica localhost come nome server, la gestione connessione stabilisce una connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer locale. Per utilizzare un'istanza remota di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sostituire localhost con il nome del server a cui si desidera connettersi.  
  
4.  Verificare che l'opzione **Usa autenticazione di Windows** sia selezionata nel gruppo **Accesso al server** .  
  
5.  Nella casella **selezionare o immettere un nome di database** nel gruppo **Connetti a un database** Digitare o selezionare `AdventureWorksDW2012` .  
  
6.  Fare clic su **Test connessione** per verificare che le impostazioni di connessione specificate siano valida.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic su **OK**.  
  
9. Nel riquadro **Connessioni dati** della finestra di dialogo **Configura gestione connessione OLE DB** verificare che sia selezionato **localhost.AdventureWorksDW2012** .  
  
10. Fare clic su **OK**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 4: Aggiunta di un'attività Flusso di dati al pacchetto](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Vedere anche  
 [gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
