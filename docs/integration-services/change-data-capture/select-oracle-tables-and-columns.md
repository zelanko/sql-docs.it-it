---
title: Selezionare tabelle e colonne Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0d550361063bd051e146b8fc350ae63b0b57c399
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728562"
---
# <a name="select-oracle-tables-and-columns"></a>Selezionare tabelle e colonne Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la pagina Seleziona tabelle e colonne Oracle per selezionare le tabelle dal database di origine Oracle in cui vengono acquisite le modifiche. Nella pagina sono presenti gli elementi seguenti:  
  
## <a name="options"></a>Opzioni  
 **Elenco tabelle**  
 Nell'elenco tabelle sono presenti tre colonne:  
  
-   **Nome tabella Oracle**: nome della tabella, incluso lo schema.  
  
-   **Istanza di acquisizione**: nome dell'istanza di acquisizione usata per denominare gli oggetti Change Data Capture specifici dell'istanza. L'istanza di acquisizione non può essere NULL.  
  
     Se non è specificato, il nome deriva dal nome dello schema di origine più il nome della tabella di origine nel formato `<schema-name>_<table-name>`. Il nome dell'istanza di acquisizione non può superare i 100 caratteri e deve essere univoco nel database.  
  
     È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **capture_instance**.  
  
-   **Ruolo di sicurezza**: nome del ruolo del database usato per controllare l'accesso ai dati delle modifiche.  
  
     È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **security_role**.  
  
 **Aggiungi tabelle**  
 Fare clic su **Aggiungi tabelle** per aprire la finestra di dialogo Selezione tabelle in cui è possibile [Selezionare le tabelle Oracle per l'acquisizione delle modifiche](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md).  
  
 **Modifica**  
 Selezionare una tabella dall'elenco e selezionare **Modifica** per aprire la finestra di dialogo **Proprietà** per tale tabella in cui è possibile [Apportare modifiche alle tabelle selezionate per l'acquisizione di modifiche](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md).  
  
 **Rimuovi**  
 Selezionare una tabella dall'elenco e fare clic su **Rimuovi** per rimuovere la tabella dall'istanza di CDC.  
  
 Dopo aver [selezionato le tabelle Oracle per l'acquisizione delle modifiche](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md) e/o [apportato modifiche alle tabelle selezionate per l'acquisizione di modifiche](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md) usando le finestre di dialogo corrette, fare clic su **Avanti** e passare a [Generare ed eseguire lo script di registrazione supplementare](../../integration-services/change-data-capture/generate-and-run-the-supplemental-logging-script.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Modificare le tabelle](../../integration-services/change-data-capture/edit-tables.md)   
 [Aggiungere tabelle a un'istanza di CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)   
 [Modificare le proprietà delle tabelle](../../integration-services/change-data-capture/edit-the-table-properties.md)  
  
  
