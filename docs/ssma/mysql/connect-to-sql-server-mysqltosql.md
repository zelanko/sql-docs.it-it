---
title: Connetti a SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d73abd3a-80df-4293-b973-1723069db049
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8dc64c84a8d14ea86893d52044894e0af2b1a3bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103209"
---
# <a name="connect-to-sql-server-mysqltosql"></a>Connettersi a SQL Server (MySQLToSQL)
Utilizzare la finestra di dialogo **Connetti a SQL Server** per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera eseguire la migrazione. Per accedere alla finestra di dialogo **Connetti a SQL Server** , scegliere **Connetti a SQL Server**dal menu **file** .  
  
## <a name="options"></a>Opzioni  
**Nome server**  
Consente di immettere o selezionare l'istanza di SQL Server a cui connettersi. Per impostazione predefinita, viene visualizzata l'istanza di connessa più di recente.  
  
-   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
-   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
-   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer, una barra rovesciata e il nome dell'istanza, ad esempio *MyServer*\\*istanza*.  
  
**Porta server**  
Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è configurata in modo da accettare le connessioni sulla porta predefinita (1433), immettere il numero di porta. In caso contrario, lasciare vuoto questo valore.  
  
**Database**  
Consente di specificare il database in cui eseguire la migrazione di oggetti e dati. Questa opzione non è disponibile quando si esegue la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**autenticazione**  
Selezionare il metodo di autenticazione utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per utilizzare l'account di Windows corrente, selezionare autenticazione di Windows. Per specificare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso e una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] password, selezionare autenticazione.  
  
**Nome utente**  
Se si utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, immettere l'account di accesso per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l'istanza di. Se si utilizza l'autenticazione di Windows, questa opzione non è disponibile.  
  
**Password**  
Se si utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, immettere la password per l'account di accesso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tale istanza di. Se si utilizza l'autenticazione di Windows, questa opzione non è disponibile.  
  
**Encrypt Connection**  
Se si desidera connettersi in modo sicuro a SQL Server, utilizzare la casella di controllo Crittografa connessione selezionando la casella di controllo **Crittografa connessione** .  
  
**TrustServerCertificate**  
Se si desidera utilizzare questa opzione, selezionare la casella di controllo **certificato server attendibile** .  
  
> [!NOTE]  
> Per abilitare il **certificato del server di attendibilità**, "Encrypt" deve essere impostato su **true**.  
  
