---
title: Servizio sconosciuto (scheda Accesso)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8fae62bb72e41cd9f87200a6bcfd2f17eb780697
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307598"
---
# <a name="unknown-service-log-on-tab"></a>Servizio sconosciuto (scheda Accesso)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non riesce a identificare il servizio.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riceve informazioni sul servizio dal provider WMI del computer in cui il servizio è in esecuzione. Si è verificato un errore durante la lettura delle proprietà del servizio oppure tali proprietà non sono complete. Per risolvere questo problema, provare a chiudere e riaprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure controllare il provider WMI nel computer in cui viene eseguito il servizio.  
  
 Il provider WMI è un componente di Windows. Per informazioni su come controllare le autorizzazioni per il provider WMI, vedere "Procedura: Configurare WMI per mostrare lo stato del server in Strumenti SQL Server" nella documentazione online di SQL Server.  
  
 Se si ritiene che il servizio visualizzato sia corretto, utilizzare la scheda **Accesso** della finestra di dialogo **Proprietà - Servizio sconosciuto** per specificare l'account utilizzato dal servizio e per avviare e arrestare il servizio.  
  
## <a name="options"></a>Opzioni  
 **Account di sistema locale**  
 Specificare un account di sistema locale che non richiede una password. Tuttavia, a seconda dei privilegi concessi, l'account di sistema locale può impedire le interazioni tra il servizio e gli altri server.  
  
 **Account seguente**  
 Specificare un account utente locale o di dominio che utilizza l’autenticazione di Windows. È consigliabile usare un account utente di dominio con diritti minimi per i servizi. Per ulteriori informazioni sulla selezione di un account, vedere "Impostazione di account di servizio Windows" nella documentazione online di SQL Server.  
  
 **Account Name** (Nome account)  
 Specificare il nome dell'account utente locale o di dominio.  
  
 **Password**  
 Digitare la password dell'account.  
  
 **Conferma password**  
 Digitare nuovamente la password dell'account.  
  
 **Inizia**  
 Avviare il servizio.  
  
 **Stop**  
 Consente di arrestare il servizio.  
  
 **Sospendi**  
 Consente di sospendere il servizio.  
  
 **Riprendi**  
 Consente di riprendere un servizio sospeso.  
  
  
