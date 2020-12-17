---
title: Proprietà - Analysis Server (scheda Servizio)
description: Informazioni sulle opzioni disponibili nella scheda Servizio della finestra di dialogo Proprietà computer Analysis Server, ad esempio il percorso binario, il nome host e la modalità di avvio.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 8dbe4bc5-6aa9-48ee-857e-0b4ea764b9cb
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: de79d7d8392e2d63b7b0b71f34dc55e9a8254933
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463904"
---
# <a name="analysis-server-properties-service-tab"></a>Proprietà - Analysis Server (scheda Servizio)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
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
 Visualizza il tipo di servizio fornito ai processi chiamanti. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installa diversi servizi.  
  
 **Modalità di avvio**  
 Impostare una delle opzioni seguenti per il servizio:  
  
-   Manuale: il servizio non viene avviato automaticamente all'avvio del computer. In questo caso è necessario avviare il servizio tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un altro strumento.  
  
-   Automatico: viene eseguito un tentativo automatico di avvio del servizio all'avvio del computer.  
  
-   Disabilitato: il servizio non può essere avviato.  
  
 **State**  
 Indica se il servizio è in esecuzione, arrestato o disabilitato.  
  
  
