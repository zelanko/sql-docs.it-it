---
title: Selezionare tabelle e colonne Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe951cb7811bb8cc92414564fda466657d2fae8c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384759"
---
# <a name="select-oracle-tables-and-columns"></a>Selezionare tabelle e colonne Oracle
  Utilizzare la pagina Seleziona tabelle e colonne Oracle per selezionare le tabelle dal database di origine Oracle in cui vengono acquisite le modifiche. Nella pagina sono presenti gli elementi seguenti:  
  
## <a name="options"></a>Opzioni  
 **Elenco tabelle**  
 Nell'elenco tabelle sono presenti tre colonne:  
  
-   **Nome tabella Oracle**: Il nome della tabella, inclusi lo schema della tabella.  
  
-   **Istanza di acquisizione**: Il nome dell'istanza di acquisizione utilizzato per oggetti di nome specifico dell'istanza change data capture. L'istanza di acquisizione non può essere NULL.  
  
     Se non è specificato, il nome deriva dal nome dello schema di origine più il nome della tabella di origine nel formato `<schema-name>_<table-name>`. Il nome dell'istanza di acquisizione non può superare i 100 caratteri e deve essere univoco nel database.  
  
     È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **capture_instance**.  
  
-   **Ruolo di sicurezza**: Nome del ruolo utilizzato per controllare l'accesso ai dati delle modifiche del database.  
  
     È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **security_role**.  
  
 **Aggiungi tabelle**  
 Fare clic su **Aggiungi tabelle** per aprire la finestra di dialogo Selezione tabelle in cui è possibile [Selezionare le tabelle Oracle per l'acquisizione delle modifiche](select-oracle-tables-for-capturing-changes.md).  
  
 **Modifica**  
 Selezionare una tabella dall'elenco e selezionare **Modifica** per aprire la finestra di dialogo **Proprietà** per tale tabella in cui è possibile [Apportare modifiche alle tabelle selezionate per l'acquisizione di modifiche](make-changes-to-the-tables-selected-for-capturing-changes.md).  
  
 **Rimuovi**  
 Selezionare una tabella dall'elenco e fare clic su **Rimuovi** per rimuovere la tabella dall'istanza di CDC.  
  
 Dopo aver [selezionato le tabelle Oracle per l'acquisizione delle modifiche](select-oracle-tables-for-capturing-changes.md) e/o [apportato modifiche alle tabelle selezionate per l'acquisizione di modifiche](make-changes-to-the-tables-selected-for-capturing-changes.md) usando le finestre di dialogo corrette, fare clic su **Avanti** e passare a [Generare ed eseguire lo script di registrazione supplementare](generate-and-run-the-supplemental-logging-script.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Modificare le tabelle](edit-tables.md)   
 [Aggiungere tabelle a un'istanza di CDC](add-tables-to-a-cdc-instance.md)   
 [Modificare le proprietà delle tabelle](edit-the-table-properties.md)  
  
  
