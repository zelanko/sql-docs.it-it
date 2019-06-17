---
title: Modificare il mapping dei tipi (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 98b7c0433e506d7ef6e825199a9a6629c52e6f3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183089"
---
# <a name="edit-type-mapping-mysqltosql"></a>Modificare il mapping dei tipi (MySQLToSQL)
Il **modifica del mapping dei tipi** nella finestra di dialogo consente di specificare la modalità di mapping dei tipi tra gli oggetti di database di origine e destinazione.  
  
È possibile accedere a questa finestra di dialogo in diverse posizioni:  
  
-   Quando si seleziona un database di origine o di un oggetto di database, il **Mapping dei tipi** verrà visualizzata la scheda a destra della finestra di esplorazione di metadati. Fare clic su **Add** per aggiungere un nuovo mapping dei tipi, o fare clic su **modificare** per modificare un mapping di tipo esistente.  
  
-   Nel **Tools** dal menu **le impostazioni del progetto** o **impostazioni di progetto predefinite**. Nella finestra di dialogo visualizzata, selezionare **Mapping dei tipi**. Fare clic su **Add** per aggiungere un nuovo mapping dei tipi, o fare clic su **modificare** per modificare un mapping di tipo esistente.  
  
-   Mapping dei tipi di tabella specifiche di eseguire l'override del database e i mapping dei tipi di progetto. Mapping di specifiche del database di eseguire l'override dei mapping di progetto.  
  
## <a name="options"></a>Opzioni  
  
##### <a name="source-type"></a>Tipo di origine  
Selezionare il tipo di dati di origine per eseguire il mapping a un tipo di dati di SQL Server.  
  
Se il tipo di dati è di lunghezza variabile, i campi seguenti verranno visualizzati sotto **Sourcetype**:  
  
##### <a name="from"></a>From  
Specificare la lunghezza minima per questo mapping. Ad esempio, per il **nchar** tipo di dati, è possibile immettere 10 per specificare che questo mapping è per un intervallo inizi a **nchar (10).**  
  
##### <a name="to"></a>Per  
Specificare la lunghezza massima consentita per questo mapping. Ad esempio, per il **nchar** tipo di dati, è possibile immettere 20 per specificare che questo mapping è per un intervallo termina **nchar(20).**  
  
##### <a name="target-type"></a>Tipo di destinazione  
Selezionare il tipo di dati di SQL Server a cui viene eseguito il mapping al tipo di origine. Quando SSMA viene creata la tabella o in SQL Server, il tipo di dati di origine passerà a questo tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, il campo seguente verrà visualizzato nella **tipo di destinazione**:  
  
##### <a name="replace-with"></a>Sostituisci con  
Specificare la lunghezza di destinazione per questo mapping. Ad esempio, per il **nvarchar** tipo di dati, è possibile immettere 20 per specificare che il tipo di dati di origine specificato deve essere mappato a **nvarchar (20).**  
  
