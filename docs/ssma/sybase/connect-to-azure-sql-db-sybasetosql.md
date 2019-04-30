---
title: Connettersi al database SQL di Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 057a39fd393be6cce9232d787b0d110a4be2035a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63060994"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Connettersi al database SQL di Azure (SybaseToSQL)
Usare la connessione alla finestra di dialogo di database SQL di Azure per la connessione al database che si desidera eseguire la migrazione di database SQL di Azure.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connetti al database SQL di Azure**. Se si è già connessa, il comando è **riconnessione al database SQL di Azure.**  
  
## <a name="options"></a>Opzioni  
**Nome server**  
  
Selezionare o immettere il nome del Server per la connessione al database SQL di Azure.  
  
**Database**  
  
Selezionare, inserire o **esplorare** il nome del Database.  
  
> [!IMPORTANT]  
> SSMA per Sybase non supporta la connessione al database master nel database SQL di Azure.  
  
**Nome utente**  
  
Immettere il nome utente utilizzato per connettersi al database di Azure SQL DB SSMA  
  
**Password**  
  
Immettere la password associata al nome utente.  
  
**Encrypt**  
  
SSMA consiglia connessione crittografata al database SQL di Azure.  
  
## <a name="create-azure-database"></a>Creare il Database di Azure  
Se non sono disponibili database nell'account di database SQL di Azure, è possibile creare il primo database.  
  
Per creare un nuovo database per la prima volta, seguire la procedura seguente  
  
1.  Fare clic sul pulsante Sfoglia, che è presente nella finestra Connetti alla finestra di dialogo di database SQL di Azure  
  
2.  Se non sono presenti database, vengono visualizzati i seguenti due voci di menu.  
  
    1.  **(Nessun database trovato)**  che è disabilitata e continuamente in grigio  
  
    2.  **Crea nuovo database** che è abilitato solo quando non sono presenti database nell'account di database SQL di Azure. Facendo clic su questa voce di menu, finestra di dialogo Crea Database di Azure è presente con dimensioni e il nome del database.  
  
3.  Al momento della creazione del database, i due parametri seguenti vengono forniti come input:  
  
    1.  **Nome del database:** Immettere il nome del Database.  
  
    2.  **Dimensioni del database:** Selezionare le dimensioni del Database che è necessario creare account di database SQL di Azure.  
  
