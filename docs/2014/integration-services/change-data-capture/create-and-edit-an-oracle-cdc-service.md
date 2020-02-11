---
title: Creare e modificare un servizio Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b59ebbf4bb56d23009351f4a8fb7f193a59fa66
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771447"
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>Creare e modificare un servizio Oracle CDC
  Da CDC Service Configuration Console viene creato e modificato un nuovo servizio Windows di Oracle CDC.  
  
 Per creare un nuovo servizio Windows di Oracle CDC, selezionare **Local CDC Services** dal riquadro sinistro, quindi fare clic su **New service** nel riquadro **Actions** . È inoltre possibile fare clic con il pulsante destro del mouse su **Local CDC Services** (Servizi CDC locali) e selezionare **New Service**(Nuovo servizio). Verrà aperta la finestra di dialogo New Oracle CDC Windows Service.  
  
 **OR**  
  
 Per modificare le proprietà del servizio CDC, selezionare il servizio di cui si desidera modificare le proprietà e fare clic su **Properties** dal riquadro **Actions** . È inoltre possibile fare clic con il pulsante destro del mouse sul servizio usato e selezionare **Properties**. Verrà visualizzata la finestra di dialogo CDC Service Properties.  
  
 Immettere le informazioni seguenti nella finestra di dialogo New Oracle CDC Windows Service CDC o la finestra di dialogo CDC Service Properties.  
  
 Nome servizio  
 Digitare il nome del nuovo servizio Windows di Oracle CDC. Non utilizzare nomi lunghi, se possibile. Non è possibile utilizzare i caratteri / e \ nel nome del servizio.  
  
> [!NOTE]  
> Questa opzione non è disponibile quando si modifica il servizio. Non è possibile modificare il nome di un servizio Windows già esistente.  
  
 **Descrizione**  
 Digitare una descrizione del servizio per consentirne l'identificazione.  
  
 **Account servizio**  
 Selezionare una delle opzioni seguenti per determinare con quale account verrà eseguito il servizio:  
  
-   **Account Sistema locale**  
  
     Non è consigliabile scegliere questa opzione perché fornisce troppo autorizzazioni al servizio.  
  
-   **This Account**  
  
     In Windows Vista o Windows Server 2008, l'account del servizio predefinito è NETWORK SERVICE.  
  
     In Windows 7, Windows Server 2008 R2 e versioni successive, l'account del servizio predefinito è Servizio NT\\<nome-servizio>.  
  
     Con questi account è possibile evitare l'utilizzo delle password in quanto non sono necessarie per questi account. Inoltre, questi account forniscono solo le autorizzazioni necessarie richieste per l'esecuzione del servizio Oracle CDC.  
  
     È possibile utilizzare un account di Windows locale o di dominio per l'account del servizio. In questo caso, è necessario immettere un valore in **Password** per l'account. Questo account può essere per l'host locale o un account di dominio. Assicurarsi di aggiornare la password quando viene modificata utilizzando Servizi locali nel Pannello di controllo di Windows.  
  
 **Nome server**: selezionare l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione a cui connettersi, ad esempio, **\\\\<nome_computer>\\<nome_istanza>** . Per impostazione predefinita verrà visualizzata l'ultima istanza del server a cui è stata effettuata la connessione.  
  
 **autenticazione**  
 Selezionare uno degli elementi seguenti:  
  
-   **Windows Authentication**: se si seleziona questa opzione, il servizio Oracle CDC si connette all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione usando l'identità dell'account del servizio. Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in un computer diverso, è necessario utilizzare l'autenticazione di Windows con gli account di dominio.  
  
-   **Autenticazione di SQL Server**: se si seleziona questa opzione, è necessario digitare **Nome utente** e **Password** per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da usare. Il servizio Oracle CDC utilizza queste credenziali per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 È sufficiente che l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dal servizio Oracle CDC sia membro del ruolo predefinito del server pubblico, non sono necessari altri privilegi. Una volta aggiunte nuove istanze di Oracle CDC, l'account di accesso otterrà l'accesso **db_owner** ai database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC associati.  
  
 Per creare la definizione del servizio Windows di Oracle CDC, è necessario aggiornare l'accesso al database MSXDBCDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata. Quando si fa clic su **OK**, una finestra di dialogo richiede all'utente di immettere un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un accesso aggiornato al database MSXDBCDC.  
  
 Per informazioni sui dati da digitare nella finestra di dialogo Connect to SQL Server, vedere [Connection to SQL Server](connection-to-sql-server.md).  
  
 **Opzioni**  
 Fare clic sulla freccia per visualizzare le opzioni disponibili da configurare. È possibile scegliere di non modificare il valore predefinito per queste opzioni. Sono disponibili le opzioni seguenti:  
  
-   **Connection Timeout** (Timeout connessione): Digitare il tempo, in secondi, di attesa del servizio CDC per Oracle per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima che si verifichi un errore di timeout. Il valore predefinito è **15**.  
  
-   **Timeout connessione** (Timeout esecuzione): Digitare il tempo, in secondi, di attesa del servizio Windows Oracle CDC per l'esecuzione di un comando prima che si verifichi un errore di timeout. Il valore predefinito è **30**.  
  
-   **Encrypt Connection** (Crittografia connessione): selezionare **Encrypt Connection** (Crittografa connessione) per la comunicazione tra il servizio Oracle CDC e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione tramite una connessione crittografata.  
  
-   **Avanzate**: digitare eventuali proprietà di connessione aggiuntive, se necessario.  
  
 **Master Password**  
 Immettere una password che verrà utilizzata dal servizio Windows di Oracle CDC per proteggere le credenziali di log mining Oracle.  
  
 La stessa password master deve inoltre essere utilizzata quando le altre istanze dello stesso servizio sono configurate in altri nodi di un cluster con configurazione di disponibilità elevata. Se si perde o si modifica la password master, è necessario immettere nuovamente tutte le password di log mining archiviate nei database dell'istanza di Oracle CDC utilizzando CDC Designer Console.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione e modifica di un servizio CDC](how-to-create-and-edit-a-cdc-service.md)  
  
  
