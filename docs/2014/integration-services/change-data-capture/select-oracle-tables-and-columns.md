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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: af7f97d7d1671aada299b685981e81d62010df24
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788344"
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
  
  
