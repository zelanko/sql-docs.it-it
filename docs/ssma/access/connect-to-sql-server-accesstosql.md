---
title: Connettersi a SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ceb77a97-d6d5-4a92-90a6-342e97d12b54
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 006a90ca082861aea4fecbe6934947afa2020335
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006665"
---
# <a name="connect-to-sql-server-accesstosql"></a>Connettersi a SQL Server (AccessToSQL)
Usare la **Connetti al Server SQL** finestra di dialogo per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si desidera eseguire la migrazione a. Per l'accesso di **Connetti al Server SQL** finestra di dialogo il **File** dal menu fare clic su **Connetti a SQL Server**.  
  
## <a name="options"></a>Opzioni  
**Nome server**  
Immettere o selezionare l'istanza di SQL Server a cui connettersi. Per impostazione predefinita, viene visualizzata l'istanza che connesso a più di recente.  
  
-   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto ( **.** ).  
  
-   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
-   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer, una barra rovesciata e il nome dell'istanza, ad esempio *MyServer*\\*MyInstance*.  
  
**Porta server**  
Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è configurato per accettare connessioni abilitata l'impostazione predefinita la porta (1433), immettere il numero di porta. In caso contrario, lasciare vuoto questo valore.  
  
**Database**  
Specificare il database per eseguire la migrazione di oggetti e dati. Questa opzione non è disponibile durante la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Autenticazione**  
Selezionare il metodo di autenticazione usato per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per usare l'account di Windows corrente, selezionare l'autenticazione di Windows. Per specificare una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso e password, selezionare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.  
  
**Nome utente**  
Se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, immettere l'account di accesso per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si usa l'autenticazione di Windows, questa opzione non è disponibile.  
  
**Password**  
Se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, immettere la password per l'account di accesso nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si usa l'autenticazione di Windows, questa opzione non è disponibile.  
  
**Encrypt Connection**  
Se si desidera connettersi in modo sicuro a SQL Server, utilizzare Crittografa connessione controllando il **Crittografa connessione** casella di controllo.  
  
**TrustServerCertificate**  
Se si desidera utilizzare questa opzione, selezionare la **considera attendibile certificato Server** casella di controllo.  
  
> [!NOTE]  
> Per abilitare **considera attendibile certificato Server**, "Crittografa" deve essere impostata su **True**.  
  
