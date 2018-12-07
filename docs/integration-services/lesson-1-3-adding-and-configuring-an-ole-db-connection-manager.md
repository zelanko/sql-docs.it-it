---
title: 'Passaggio 3: Aggiunta e configurazione di una gestione connessione OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3fbb4994b1f7f7416fbdbdde5dc6377b396dae9a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539075"
---
# <a name="lesson-1-3---adding-and-configuring-an-ole-db-connection-manager"></a>Lezione 1-3 - Aggiunta e configurazione di una gestione connessione OLE DB
Dopo aver aggiunto una gestione connessione file flat per connettersi all'origine dati, l'operazione successiva consiste nell'aggiunta di una gestione connessione OLE DB per connettersi alla destinazione. Una gestione connessione OLE DB abilita un pacchetto all'estrazione di dati o al caricamento di dati in un'origine dati compatibile con OLE DB. Gestione connessione OLE DB consente di specificare il server, il metodo di autenticazione e il database predefinito per la connessione.  
  
In questa lezione verrà creata una gestione connessione OLE DB tramite cui viene utilizzata l'autenticazione di Windows per connettersi all'istanza locale di **AdventureWorksDB2012**. Alla gestione connessione OLE DB creata faranno anche riferimento altri componenti che verranno creati più avanti in questa esercitazione, come la trasformazione Ricerca e la destinazione OLE DB.  
  
### <a name="add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Aggiungere e configurare una gestione connessione OLE DB nel pacchetto SSIS  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area **Gestioni connessioni** e quindi fare clic su **Nuova connessione OLE DB**.  
  
2.  Nella finestra di dialogo **Configura gestione connessione OLE DB** fare clic su **Nuova**.  
  
3.  Per **Nome server**, immettere **localhost**.  
  
    Quando si specifica localhost come nome server, la gestione connessione stabilisce una connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer locale. Per utilizzare un'istanza remota di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sostituire localhost con il nome del server a cui si desidera connettersi.  
  
4.  Verificare che l'opzione **Usa autenticazione di Windows** sia selezionata nel gruppo **Accesso al server** .  
  
5.  Nella casella **Selezionare o immettere un nome di database** del gruppo **Connessione al database** digitare o selezionare **AdventureWorksDW2012**.  
  
6.  Fare clic su **Test connessione** per verificare che le impostazioni di connessione specificate siano valida.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic su **OK**.  
  
9. Nel riquadro **Connessioni dati** della finestra di dialogo **Configura gestione connessione OLE DB** verificare che sia selezionato **localhost.AdventureWorksDW2012** .  
  
10. Fare clic su **OK**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Passaggio 4: Aggiunta di un'attività Flusso di dati al pacchetto](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Vedere anche  
[Gestione connessione OLE DB](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
