---
title: Finestra di dialogo Configura log SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f881435de01c7c21b80bff00b43c2399d0f7d75
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060586"
---
# <a name="configure-ssis-logs-dialog-box"></a>Configura log SSIS - finestra di dialogo
  Utilizzare la finestra di dialogo **Configura log SSIS** per definire le opzioni di registrazione per un pacchetto.  
  
 **Per saperne di più**  
  
1.  [Apertura della finestra di dialogo Configura log SSIS](#open_dialog)  
  
2.  [Configurazione delle opzioni nel riquadro Contenitori](#container)  
  
3.  [Configurazione delle opzioni nella scheda Provider e log](#provider)  
  
4.  [Configurazione delle opzioni nella scheda Dettagli](#detail)  
  
##  <a name="open-the-configure-ssis-logs-dialog-box"></a><a name="open_dialog"></a>Aprire la finestra di dialogo Configura log SSIS  
 **Per aprire la finestra di dialogo Configura log SSIS**  
  
-   In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] scegliere **Registrazione** nel menu **SSIS** .  
  
##  <a name="configure-the-options-in-the-containers-pane"></a><a name="container"></a>Configurare le opzioni nel riquadro Contenitori  
 Utilizzare il riquadro **Contenitori** della finestra di dialogo **Configura log SSIS** per abilitare il pacchetto e i relativi contenitori per la registrazione.  
  
### <a name="options"></a>Opzioni  
 **Contenitori**  
 Nella visualizzazione gerarchica selezionare le caselle di controllo in modo da abilitare il pacchetto e i relativi contenitori per la registrazione:  
  
-   Se deselezionato, il contenitore non è abilitato per la registrazione. Selezionarlo per abilitare la registrazione.  
  
-   Se visualizzato in grigio, il contenitore utilizza le opzioni di registrazione dell'elemento padre. Questa opzione non è disponibile per il pacchetto.  
  
-   Se selezionato, il contenitore definisce opzioni di registrazione specifiche.  
  
 Se si desidera impostare le opzioni di registrazione per un contenitore visualizzato in grigio, fare doppio clic sulla casella di controllo corrispondente al contenitore in questione. Al primo clic la casella di controllo viene deselezionata e al secondo clic viene selezionata, consentendo di scegliere il provider di log da utilizzare e di specificare le informazioni da registrare.  
  
##  <a name="configure-the-options-on-the-providers-and-logs-tab"></a><a name="provider"></a>Configurare le opzioni nella scheda provider e log  
 Usare la scheda **Provider e log** della finestra di dialogo **Configura log SSIS** per creare e configurare log per l'acquisizione di eventi di runtime.  
  
### <a name="options"></a>Opzioni  
 **Tipo provider**  
 Consente di selezionare un tipo di logger nell'elenco.  
  
 **Aggiungere**  
 Consente di aggiungere un log del tipo specificato alla raccolta di logger del pacchetto.  
  
 **Nome**  
 Consente di abilitare o disabilitare log per contenitori o attività selezionati nel riquadro **Contenitori** della finestra di dialogo **Configura log SSIS** usando le caselle di controllo. Il campo del nome è modificabile. Utilizzare il nome predefinito per il provider oppure digitare un nome descrittivo univoco.  
  
 **Descrizione**  
 Il campo della descrizione è modificabile. Fare clic nel campo e quindi modificare la descrizione predefinita del log.  
  
 **Configurazione**  
 Selezionare una gestione connessione esistente nell'elenco oppure fare clic su \< **nuova connessione...**> per creare una nuova gestione connessione. A seconda del tipo di logger, è possibile configurare una gestione connessione OLE DB o una gestione connessione file. Il logger per il registro eventi di [!INCLUDE[msCoName](../includes/msconame-md.md)] non necessita di connessioni.  
  
 Argomenti correlati: [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md) e [File Connection Manager](connection-manager/file-connection-manager.md)  
  
 **Elimina**  
 Selezionare un provider di log e fare clic su **Elimina**.  
  
##  <a name="configure-the-options-on-the-details-tab"></a><a name="detail"></a>Configurare le opzioni nella scheda Dettagli  
 Utilizzare la scheda **Dettagli** della finestra di dialogo **Configura log SSIS** per indicare gli eventi da abilitare per la registrazione e specificare le informazioni da registrare. Le informazioni selezionate saranno valide per tutti i provider di log nel pacchetto. Non è ad esempio possibile scrivere informazioni nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] diverse da quelle specificate in un file di testo.  
  
### <a name="options"></a>Opzioni  
 **Events**  
 Consente di abilitare o disabilitare gli eventi per la registrazione.  
  
 **Descrizione**  
 Consente di visualizzare una descrizione dell'evento.  
  
 **Avanzate**  
 Consente di selezionare o deselezionare gli eventi da registrare, nonché le informazioni da registrare per ogni evento. Fare clic su **Standard** per nascondere tutti i dettagli di registrazione, ad eccezione dell'elenco di eventi. Per la registrazione sono disponibili le informazioni seguenti:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Computer**|Nome del computer in cui si è verificato l'evento registrato.|  
|**Operatore**|Nome utente dell'utente che ha avviato il pacchetto.|  
|**SourceName**|Nome del pacchetto, contenitore o attività in cui si è verificato l'evento registrato.|  
|**SourceID**|Identificatore univoco globale (GUID, Global Unique Identifier) del pacchetto, contenitore o attività in cui si è verificato l'evento registrato.|  
|**ExecutionID**|Identificatore univoco globale dell'istanza di esecuzione del pacchetto.|  
|**MessageText**|Messaggio associato alla voce di log.|  
|**DataBytes**|Riservato per utilizzi futuri.|  
  
 **Basic**  
 Consente di selezionare o deselezionare gli eventi da registrare. Questa opzione può essere utilizzata per nascondere i dettagli di registrazione, ad eccezione dell'elenco di eventi. Se si seleziona un evento, per impostazione predefinita verranno selezionati anche tutti i relativi dettagli di registrazione. Fare clic su **Avanzate** per visualizzarli.  
  
 **Carica**  
 Consente di specificare un file XML esistente da utilizzare come modello per l'impostazione delle opzioni di registrazione.  
  
 **Salva**  
 Consente di salvare i dettagli di configurazione come modello in un file XML.  
  
  
