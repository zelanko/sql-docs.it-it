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
ms.openlocfilehash: be592319f63bca6d0de8c5e19def97849a0ec355
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84922477"
---
# <a name="select-oracle-tables-and-columns"></a>Selezionare tabelle e colonne Oracle
  Utilizzare la pagina Seleziona tabelle e colonne Oracle per selezionare le tabelle dal database di origine Oracle in cui vengono acquisite le modifiche. Nella pagina sono presenti gli elementi seguenti:  
  
## <a name="options"></a>Opzioni  
 **Elenco Tabella**  
 Nell'elenco tabelle sono presenti tre colonne:  
  
-   **Nome tabella Oracle**: nome della tabella, incluso lo schema.  
  
-   **Istanza di acquisizione**: nome dell'istanza di acquisizione usato per denominare gli oggetti Change Data Capture specifici dell'istanza. L'istanza di acquisizione non può essere NULL.  
  
     Se non è specificato, il nome deriva dal nome dello schema di origine più il nome della tabella di origine nel formato `<schema-name>_<table-name>`. Il nome dell'istanza di acquisizione non può superare i 100 caratteri e deve essere univoco nel database.  
  
     È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **capture_instance**.  
  
-   **Ruolo di sicurezza**: nome del ruolo del database utilizzato per controllare l'accesso ai dati delle modifiche.  
  
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
  
  
