---
title: Servizio sconosciuto (scheda accesso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 686eb039660efb6e3596b9dac88fc0d24deacaee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150524"
---
# <a name="unknown-service-log-on-tab"></a>Servizio sconosciuto (scheda Accesso)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di identificare il servizio.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riceve informazioni sul servizio dal provider WMI del computer in cui il servizio è in esecuzione. Si è verificato un errore durante la lettura delle proprietà del servizio oppure tali proprietà non sono complete. Per risolvere questo problema, provare a chiudere e riaprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure controllare il provider WMI nel computer in cui viene eseguito il servizio.  
  
 Il provider WMI è un componente di Windows. Per informazioni su come controllare le autorizzazioni per il provider WMI, vedere "procedura: Configurare WMI per mostrare lo stato del Server in strumenti SQL Server"nella documentazione Online di SQL Server.  
  
 Se si ritiene che il servizio visualizzato sia corretto, utilizzare la scheda **Accesso** della finestra di dialogo **Proprietà - Servizio sconosciuto** per specificare l'account utilizzato dal servizio e per avviare e arrestare il servizio.  
  
## <a name="options"></a>Opzioni  
 **Account di sistema locale**  
 Specificare un account di sistema locale che non richiede una password. Tuttavia, a seconda dei privilegi concessi, l'account di sistema locale può impedire le interazioni tra il servizio e gli altri server.  
  
 **Account seguente**  
 Specificare un account utente locale o di dominio che utilizza l’autenticazione di Windows. È consigliabile usare un account utente di dominio con diritti minimi per i servizi. Per ulteriori informazioni sulla selezione di un account, vedere "Impostazione di account di servizio Windows" nella documentazione online di SQL Server.  
  
 **Nome account**  
 Specificare il nome dell'account utente locale o di dominio.  
  
 **Password**  
 Digitare la password dell'account.  
  
 **Conferma password**  
 Digitare nuovamente la password dell'account.  
  
 **Start**  
 Avviare il servizio.  
  
 **Arresta**  
 Consente di arrestare il servizio.  
  
 **Sospendi**  
 Consente di sospendere il servizio.  
  
 **Riprendi**  
 Consente di riprendere un servizio sospeso.  
  
  
