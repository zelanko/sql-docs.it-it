---
title: Modificare le tabelle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c80f562b36e775ebcbbb3dd30a97fdb0bf61cb9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385979"
---
# <a name="edit-tables"></a>Modificare le tabelle
  Utilizzare la scheda **Tabelle** per apportare modifiche alle tabelle e alle colonne selezionate dal database di origine Oracle. Nella scheda sono presenti gli elementi seguenti:  
  
 **Elenco Tabella**  
 Nell'elenco tabelle sono presenti tre colonne:  
  
-   **Nome tabella Oracle**: Il nome della tabella, inclusi lo schema della tabella.  
  
-   **Istanza di acquisizione**: Il nome dell'istanza di acquisizione utilizzato per oggetti di nome specifico dell'istanza change data capture. L'istanza di acquisizione non può essere NULL. Se non è specificato, il nome deriva dal nome dello schema di origine più il nome della tabella di origine nel formato `<schema-name>_<table-name>.` Il nome dell'istanza di acquisizione non può superare i 100 caratteri e deve essere univoco nel database. È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **capture_instance**.  
  
-   **Ruolo di sicurezza**: Il nome del ruolo del database utilizzato per ottenere l'accesso ai dati delle modifiche. È possibile fare clic in qualsiasi cella di questa colonna per modificare manualmente **security_role**.  
  
 **Aggiungi tabelle**  
 Fare clic su **Aggiungi tabelle** per aprire la finestra di dialogo Selezione tabelle in cui è possibile [aggiungere tabelle a un'istanza di CDC](add-tables-to-a-cdc-instance.md). Al primo accesso di questa sessione al database Oracle, è necessario [Connect to Oracle](connect-to-oracle.md).  
  
 **Modifica**  
 Selezionare una tabella dall'elenco e selezionare **Modifica** per aprire la finestra di dialogo **Proprietà** per tale tabella in cui è possibile [Modificare le proprietà della tabella](edit-the-table-properties.md).  
  
> [!NOTE]  
>  Non è possibile modificare il mapping dei tipi per le tabelle che dispongono già di tabelle mirror. Questa operazione è possibile unicamente per le tabelle nuove.  
  
 **Rimuovi**  
 Selezionare una tabella dall'elenco e fare clic su **Rimuovi** per rimuovere la tabella dall'istanza di CDC.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di modifica delle proprietà dell'istanza di CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Selezionare tabelle e colonne Oracle](select-oracle-tables-and-columns.md)  
  
  
