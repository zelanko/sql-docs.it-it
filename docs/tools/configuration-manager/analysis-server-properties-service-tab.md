---
title: Proprietà - Analysis Server (scheda Servizio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 8dbe4bc5-6aa9-48ee-857e-0b4ea764b9cb
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: bd7dfe9da50642952c927465430cca7f8a54bb10
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729977"
---
# <a name="analysis-server-properties-service-tab"></a>Proprietà - Analysis Server (scheda Servizio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Si tratta del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Questo servizio deve essere eseguito affinché [!INCLUDE[ssAS](../../includes/ssas-md.md)] funzioni in modo corretto. I valori delle proprietà visualizzati in grigio chiaro non possono essere modificati con questa applicazione.  
  
## <a name="options"></a>Opzioni  
 **Percorso binario**  
 Visualizza il percorso dei file di programma utilizzati dal servizio.  
  
 **Controllo errori**  
 1 indica `SERVICE_ERROR_NORMAL`. In caso di problemi di avvio del servizio durante l'avvio del computer, il programma di avvio registra l'errore e visualizza una finestra di messaggio popup ma continua l'operazione di avvio. Questo valore non può essere modificato.  
  
 **Codice di uscita**  
 Quando si verifica un errore, il numero dell'errore viene visualizzato in questa casella. Questo numero può risultare utile per la risoluzione dei problemi. È possibile cercarlo nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base oppure comunicarlo al personale del supporto tecnico.  
  
 **Host Name**  
 Visualizza il nome del computer o del cluster che esegue [!INCLUDE[ssAS](../../includes/ssas-md.md)].  
  
 **Nome**  
 Indica il nome visualizzato del servizio.  
  
 **ID processo**  
 Visualizza il numero usato da [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows per tenere traccia dei processi di questo programma.  
  
 **Tipo di servizio SQL Server**  
 Visualizza il tipo di servizio fornito ai processi chiamanti. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati diversi servizi.  
  
 **Modalità di avvio**  
 Impostare una delle opzioni seguenti per il servizio:  
  
-   Manuale: il servizio non viene avviato automaticamente all'avvio del computer. In questo caso è necessario avviare il servizio tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un altro strumento.  
  
-   Automatico: viene eseguito un tentativo automatico di avvio del servizio all'avvio del computer.  
  
-   Disabilitato: il servizio non può essere avviato.  
  
 **State**  
 Indica se il servizio è in esecuzione, arrestato o disabilitato.  
  
  
