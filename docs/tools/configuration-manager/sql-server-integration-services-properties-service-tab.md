---
title: Proprietà - SQL Server Integration Services (scheda Servizio)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e6b25e14ebc6f757239046987e338d941c3fbbd8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75304948"
---
# <a name="sql-server-integration-services-properties-service-tab"></a>Proprietà - SQL Server Integration Services (scheda Servizio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Usare la scheda **Servizio** nella finestra di dialogo **Proprietà** di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per visualizzare o specificare le opzioni seguenti.  
  
## <a name="options"></a>Opzioni  
 **Percorso binario**  
 Visualizza il percorso dei file di programma utilizzati dal servizio.  
  
 **Controllo errori**  
 1 indica `SERVICE_ERROR_NORMAL`. In caso di problemi di avvio del servizio durante l'avvio del computer, il programma di avvio registra l'errore e visualizza una finestra di messaggio popup ma continua l'operazione di avvio. Questo valore non può essere modificato.  
  
 **Codice di uscita**  
 Codice di errore di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows che definisce eventuali problemi verificatisi durante l'avvio o l'arresto del servizio. Questa proprietà viene impostata su **ERROR_SERVICE_SPECIFIC_ERROR** (1066) quando l'errore è univoco per il servizio rappresentato da questa classe. Le informazioni relative all'errore sono disponibili nella proprietà **ServiceSpecificExitCode** . Il servizio imposta questo valore su NO_ERROR (0) in fase di esecuzione e di nuovo al termine.  
  
 **Host Name**  
 Visualizza il nome del computer o del cluster che esegue il servizio [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Nome**  
 Indica il nome visualizzato del servizio.  
  
 **ID processo**  
 Visualizza l'ID di processo di Windows.  
  
 **Tipo di servizio SQL Server**  
 Visualizza il tipo di servizio fornito ai processi chiamanti. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installa diversi servizi.  
  
 **Modalità di avvio**  
 Impostare una delle opzioni seguenti per il servizio:  
  
-   Manuale: il servizio non viene avviato automaticamente all'avvio del computer. In questo caso è necessario avviare il servizio tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un altro strumento.  
  
-   Automatico: viene eseguito un tentativo automatico di avvio del servizio all'avvio del computer.  
  
-   Disabilitato: il servizio non può essere avviato.  
  
 **State**  
 Indica se il servizio è in esecuzione, arrestato o disabilitato. " **...** " indica una modifica di stato in sospeso.  
  
  
