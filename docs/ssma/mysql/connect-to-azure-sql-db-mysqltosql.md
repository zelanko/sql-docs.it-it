---
title: Connettersi ad Azure SQL database (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 12da1aa42f468b92e1833410e635183aabf3a384
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103239"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Connettersi al database SQL di Azure (MySQLToSQL)
Usare la connessione alla finestra di dialogo di SQL Azure per la connessione al database di SQL Azure che si desidera eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connetti a SQL Azure**. Se si è già connessa, il comando è **Riconnetti a SQL Azure.**  
  
## <a name="options"></a>Opzioni  
**Nome server**  
  
Selezionare o immettere il nome del Server per la connessione a SQL Azure.  
  
**Database**  
  
Selezionare, inserire o **esplorare** il nome del Database.  
  
> [!IMPORTANT]  
> SSMA per MySQL supporta la connessione al database master in SQL Azure.  
  
**Nome utente**  
  
Immettere il nome utente utilizzato per connettersi al database di SQL Azure SSMA  
  
**Password**  
  
Immettere la password associata al nome utente.  
  
**Encrypt**  
  
SSMA consiglia connessione crittografata a SQL Azure.  
  
## <a name="create-azure-database"></a>Creare il Database di Azure  
Se non sono disponibili database nell'account di SQL Azure, è possibile creare il primo database.  
  
Per creare un nuovo database per la prima volta, seguire la procedura seguente  
  
1.  Fare clic sul pulsante Sfoglia, che è presente nella finestra Connetti alla finestra di dialogo di SQL Azure  
  
2.  Se non sono presenti database, vengono visualizzati i seguenti due voci di menu.  
  
    1.  **(Nessun database trovato)**  che è disabilitata e continuamente in grigio  
  
    2.  **Crea nuovo database** che è abilitato solo quando non sono presenti database nell'account di SQL Azure. Facendo clic su questa voce di menu, finestra di dialogo Crea Database di Azure è presente con dimensioni e il nome del database.  
  
3.  Al momento della creazione del database, i due parametri seguenti vengono forniti come input:  
  
    1.  **Nome del database:** Immettere il nome del Database.  
  
    2.  **Dimensioni del database:** Selezionare le dimensioni del Database che è necessario creare account di SQL Azure.  
  
