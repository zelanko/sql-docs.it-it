---
title: Connettersi al database SQL di Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0b26ddaef1373544e0df2fd9186cdf56fdafd801
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040635"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Connettersi al database SQL di Azure (AccessToSQL)
Usare la connessione alla finestra di dialogo di SQL Azure per la connessione al database di SQL Azure che si desidera eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connetti a SQL Azure**. Se si è già connessa, il comando è **Riconnetti a SQL Azure.**  
  
## <a name="options"></a>Opzioni  
**Nome server**  
  
Selezionare o immettere il nome del Server per la connessione a SQL Azure.  
  
**Database**  
  
Selezionare, inserire o **esplorare** il nome del Database.  
  
> [!IMPORTANT]  
> SSMA per Access non supporta la connessione al database master in SQL Azure.  
  
**Nome utente**  
  
Immettere il nome utente utilizzato per connettersi al database di SQL Azure SSMA  
  
**Password**  
  
Immettere la password associata al nome utente.  
  
**Encrypt**  
  
SSMA consiglia connessione crittografata a SQL Azure.  
  
## <a name="create-azure-database"></a>Creare il Database di Azure  
Per creare un nuovo database di azure, seguire questa procedura  
  
1.  Fare clic sul pulsante Sfoglia, che è presente nella finestra Connetti alla finestra di dialogo di SQL Azure  
  
2.  Se non sono presenti database, vengono visualizzate due voci di menu  
  
    1.  **(Nessun database trovato)**  che è disabilitata e continuamente in grigio  
  
    2.  **Crea nuovo database** che è sempre abilitato, consentendo all'utente di creare un nuovo database di azure nell'account di SQL Azure. Facendo clic su questa voce di menu, creare la finestra di dialogo per database di azure è disponibile, con il nome di database e le dimensioni.  
  
3.  Al momento della creazione del database, questi due parametri è passata come input.  
  
    1.  **Nome del database:** Immettere il nome del Database.  
  
    2.  **Dimensioni del database:** Selezionare le dimensioni del Database che è necessario creare account di SQL Azure.  
  
