---
title: Selezione opzioni di Gestione pacchetti (aggiornamento guidato pacchetti SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c71f254b0d0fb79e3ee8135c10d2d9ed715d3437
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056032"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>Seleziona opzioni di gestione pacchetti (Aggiornamento guidato pacchetti SSIS)
  Usare la pagina **Seleziona opzioni di gestione pacchetti** per specificare le opzioni per l'aggiornamento dei pacchetti.  
  
 **Per eseguire l'aggiornamento guidato pacchetti SSIS**  
  
-   [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna stringhe di connessione per l'uso di nuovi nomi di provider**  
 Consente di aggiornare le stringhe di connessione per utilizzare i nomi dei provider seguenti per la versione corrente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provider OLE DB per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 L'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] consente di aggiornare solo le stringhe di connessione archiviate nelle gestioni connessione. Non vengono aggiornate le stringhe di connessione costruite dinamicamente utilizzando il linguaggio delle espressioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o il codice in un'attività Script.  
  
 **Convalida pacchetti di aggiornamento**  
 Consente di convalidare i pacchetti di aggiornamento e di salvare solo i pacchetti che superano la convalida.  
  
 Se non si seleziona questa opzione, i pacchetti di aggiornamento non verranno convalidati. Pertanto, verranno salvati tutti i pacchetti di aggiornamento, indipendentemente dalla loro validità. I pacchetti di aggiornamento vengono salvati nella destinazione specificata alla pagina **Seleziona posizione di destinazione** della procedura guidata.  
  
 La convalida influisce sulla durata del processo di aggiornamento. Si consiglia di non selezionare questa opzione per pacchetti grandi che probabilmente verranno aggiornati in modo corretto.  
  
 **Crea nuovi ID pacchetto**  
 Consente di creare nuovi ID per i pacchetti di aggiornamento.  
  
 **Continua il processo di aggiornamento quando un aggiornamento del pacchetto non riesce**  
 Consente di specificare che quando un pacchetto non può essere aggiornato, l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] continua ad aggiornare i pacchetti rimanenti.  
  
 **Conflitti di nomi di pacchetto**  
 Consente di specificare come vengono gestiti i pacchetti che hanno lo stesso nome. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
 **Sovrascrivi file di pacchetto esistenti**  
 Consente di sostituire il pacchetto esistente con il pacchetto di aggiornamento con lo stesso nome.  
  
 **Aggiungi suffissi numerici a nomi di pacchetti di aggiornamento**  
 Consente di aggiungere un suffisso numerico al nome del pacchetto di aggiornamento.  
  
 **Non aggiornare i pacchetti**  
 Consente di arrestare l'aggiornamento dei pacchetti e di visualizzare un errore quando la procedura guidata viene completata.  
  
 Queste opzioni non sono disponibili quando si seleziona l'opzione **Salva in posizione di origine** nella pagina **Seleziona posizione di destinazione** della procedura guidata.  
  
 **Ignora configurazioni**  
 Consente di non caricare le configurazioni di pacchetto durante l'aggiornamento. Se si seleziona questa opzione l'aggiornamento del pacchetto richiede meno tempo.  
  
 **Esegui backup pacchetti originali**  
 Consente di eseguire il backup dei pacchetti originali in una cartella **SSISBackupFolder** . Viene creata la cartella **SSISBackupFolder** come sottocartella della cartella che contiene i pacchetti originali e i pacchetti aggiornati.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se si specifica che i pacchetti originali e i pacchetti aggiornati sono archiviati nel file system e nella stessa cartella.  
  
 Per altre informazioni, vedere [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare pacchetti di Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
