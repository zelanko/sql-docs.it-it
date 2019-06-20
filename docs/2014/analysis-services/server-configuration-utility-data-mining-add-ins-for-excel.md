---
title: Utilità di configurazione di server (dati componenti aggiuntivi Data Mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdc8434673d9220f22d31f1736bd67012653dc88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069064"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>Utilità di configurazione del server (componenti aggiuntivi data mining per Excel)
  Quando si installano i componenti aggiuntivi Data Mining per Excel, un'utilità di configurazione del Server viene installata anche e verrà eseguito alla prima che apertura di componenti aggiuntivi. In questo argomento viene descritto come utilizzare l'utilità per la connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e impostare un database per l'uso di modelli di data mining.  
  

  
##  <a name="bkmk_step1"></a> Passaggio 1: Connetti ad Analysis Services  
 Scegliere il server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che fornisce gli algoritmi di data mining e archivia i modelli di data mining.  
  
 Quando si crea una connessione per abilitare il data mining, è necessario scegliere un server in cui è possibile provare a utilizzare i modelli di data mining. È consigliabile creare un nuovo database nel server e dedicarlo al data mining oppure chiedere all'amministratore di preparare un server di data mining da utilizzare. In tal modo è possibile compilare modelli senza influire sulle prestazioni degli altri servizi.  
  
 Si noti che il server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzato per il data mining non necessariamente deve trovarsi nello stesso server dei dati di origine.  
  
 **Nome server**  
 Digitare il nome del server contenente l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che verrà utilizzata per il data mining.  
  
 **Autenticazione**  
 Specificare i metodi di autenticazione. L'autenticazione di Windows è obbligatoria per le connessioni a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a meno che l'amministratore non abbia configurato l'accesso al server tramite HTTPPump.  
  
##  <a name="bkmk_step2"></a> Passaggio 2: Consentire modelli temporanei  
 Per poter utilizzare i componenti aggiuntivi, è necessario modificare una proprietà del server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per consentire la creazione di modelli di data mining temporanei.  
  
 I modelli di data mining temporanei sono detti anche *modelli di sessione*. in quanto i modelli rimangono archiviati solo fino a quando la sessione corrente è aperta. Quando si chiude la connessione al server, la sessione viene terminata e i modelli utilizzati durante la sessione vengono eliminati.  
  
 L'utilizzo di modelli di data mining di sessione non influisce sullo spazio di archiviazione del server, mentre l'overhead causato dalla creazione di modelli di data mining può ridurre le prestazioni del server.  
  
 Durante la procedura guidata vengono innanzitutto rilevate le impostazioni specificate nel server. Se il server consente già i modelli di data mining temporanei, è possibile fare clic su **successivo** per continuare. La procedura guidata fornisce inoltre le istruzioni relative all'abilitazione dei modelli di data mining temporanei nel server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specificato o le indicazioni per effettuare una richiesta all'amministratore di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_step3"></a> Passaggio 3: Creare Database per gli utenti di componente aggiuntivo  
 In questa pagina della procedura guidata di installazione e configurazione è possibile creare un nuovo database dedicato al data mining o selezionare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esistente.  
  
> [!WARNING]  
>  Per il data mining è richiesta un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in esecuzione in modalità multidimensionale. La modalità tabulare non supporta il data mining.  
  
 È consigliabile creare un database separato dedicato al data mining. In questo modo è possibile provare a utilizzare i modelli di data mining senza influire su altri oggetti della soluzione.  
  
 Se si sceglie un database in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è possibile sovrascrivere i modelli esistenti se si utilizzano i componenti aggiuntivi per creare un modello il cui nome corrisponde a quello di un modello già esistente.  
  
 **Crea nuovo database**  
 Selezionare questa opzione per creare un nuovo database nel server selezionato. In un database di data mining vengono archiviati origini dati, strutture e modelli di data mining.  
  
 **Nome database**  
 Digitare il nome del nuovo database. Se il nome non è già in uso, verrà creato automaticamente.  
  
 **Utilizza database esistente**  
 Selezionare questa opzione per utilizzare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esistente.  
  
 **Database**  
 Se si sceglie l'opzione per utilizzare un database esistente, è necessario selezionare il nome del database nell'elenco.  
  
##  <a name="bkmk_step4"></a> Passaggio 4: Assegnazione delle autorizzazioni Appropriate agli utenti di componente aggiuntivo  
 È necessario verificare che tutti gli utenti dei componenti aggiuntivi dispongano delle autorizzazioni necessarie per esplorare, modificare, elaborare o creare strutture e modelli di data mining.  
  
 Per impostazione predefinita, per utilizzare i componenti aggiuntivi è necessaria l'autenticazione integrata di Windows.  
  
 **Concedere le autorizzazioni di amministrazione di database-gli utenti dei componenti**  
 Selezionare questa opzione per concedere l'accesso amministrativo al database agli utenti elencati.  
  
> [!NOTE]  
>  Queste autorizzazioni si applicano solo per il database indicato nel **nome del Database** casella.  
  
 **Nome database**  
 Consente di visualizzare il nome del database selezionato.  
  
 **Specificare gli utenti o gruppi da aggiungere**  
 Selezionare gli account di accesso che potranno accedere al database utilizzato per il data mining.  
  
 **Aggiungi**  
 Fare clic per aprire una finestra di dialogo e aggiungere utenti o gruppi.  
  
 **Rimuovi**  
 Fare clic per rimuovere l'utente o il gruppo selezionato dall'elenco di utenti con autorizzazioni di amministratore.  
  
  
