---
title: Connettersi al database SQL di Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7180e123572016661fa4de4a2b38a12f8480d89c
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935990"
---
# <a name="connect-to-azure-sql-database-mysqltosql"></a>Connettersi al database SQL di Azure (MySQLToSQL)
Usare la finestra di dialogo Connetti a SQL Azure per connettersi al database nel database SQL di Azure di cui si vuole eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere **Connetti a SQL Azure**dal menu **file** . Se è già stata effettuata la connessione, il comando viene **riconnesso a SQL Azure.**  
  
## <a name="options"></a>Opzioni  
**Nome server**  
  
Selezionare o immettere il nome del server per la connessione a SQL Azure.  
  
**Database**  
  
Selezionare, immettere o **esplorare** il nome del database.  
  
> [!IMPORTANT]  
> SSMA per MySQL non supporta la connessione al database master in SQL Azure.  
  
**Nome utente**  
  
Immettere il nome utente che SSMA userà per connettersi al database SQL di Azure  
  
**Password**  
  
Immettere il nome utente e la password  
  
**Encrypt**  
  
SSMA consiglia la connessione crittografata a SQL Azure.  
  
## <a name="create-azure-database"></a>Creare un database di Azure  
Se non sono presenti database nell'account di SQL Azure, è possibile creare il primo database.  
  
Per creare un nuovo database per la prima volta, attenersi alla procedura seguente:  
  
1.  Fare clic sul pulsante Sfoglia presente nella finestra di dialogo Connetti a SQL Azure  
  
2.  Se non sono presenti database, vengono visualizzate le due voci di menu seguenti.  
  
    1.  **(nessun database trovato)** disabilitato e disattivato per sempre  
  
    2.  Consente di **creare un nuovo database** abilitato solo quando non sono presenti database in SQL Azure account. Quando si fa clic su questa voce di menu, la finestra di dialogo Crea database di Azure è disponibile con nome e dimensioni del database.  
  
3.  Al momento della creazione del database, i due parametri seguenti vengono forniti come input:  
  
    1.  **Nome database:** Immettere il nome del database.  
  
    2.  **Dimensioni database:** Selezionare le dimensioni del database che è necessario creare in SQL Azure account.  
  
