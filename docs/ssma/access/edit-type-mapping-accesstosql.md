---
title: Modificare il mapping dei tipi (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7d41fc2f01e2cfbc2b20c58ea9be640f2afd8ea0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006578"
---
# <a name="edit-type-mapping-accesstosql"></a>Modifica mapping dei tipi (AccessToSQL)
La finestra di dialogo **Modifica mapping tipi** consente di specificare la modalità di mapping dei tipi tra gli oggetti di database di origine e di destinazione.  
  
È possibile accedere a questa finestra di dialogo in diverse posizioni:  
  
-   Quando si seleziona un database di origine o un oggetto di database, la scheda **mapping dei tipi** viene visualizzata a destra di Esplora metadati. Fare clic su **Aggiungi** per aggiungere un nuovo mapping dei tipi oppure fare clic su **modifica** per modificare un mapping dei tipi esistente.  
  
-   Scegliere **Impostazioni progetto** o **Impostazioni progetto predefinite**dal menu **strumenti** . Nella finestra di dialogo risultante selezionare **mapping dei tipi**. Fare clic su **Aggiungi** per aggiungere un nuovo mapping dei tipi oppure fare clic su **modifica** per modificare un mapping dei tipi esistente.  
  
I mapping dei tipi specifici della tabella sostituiscono i mapping dei tipi di progetto e di database. I mapping specifici del database sostituiscono i mapping del progetto.  
  
## <a name="options"></a>Opzioni  
**Tipo di origine**  
Consente di selezionare il tipo di dati di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il mapping a un tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, i campi seguenti verranno visualizzati in **tipo di origine**:  
  
**Da**  
Consente di specificare la lunghezza minima per questo mapping. Per il tipo di dati **Text** , ad esempio, è possibile immettere 10 per specificare che il mapping è relativo a un intervallo che inizia con il **testo (10)**.  
  
**A**  
Consente di specificare la lunghezza massima consentita per questo mapping. Per il tipo di dati **Text** , ad esempio, è possibile immettere 20 per specificare che il mapping è per un intervallo che termina con il **testo (20)**.  
  
**Tipo di destinazione**  
Consente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare il tipo di dati a cui viene eseguito il mapping del tipo di dati di origine. Quando SSMA crea la tabella o stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo di dati di origine verrà modificato in questo tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, il campo seguente verrà visualizzato in **tipo di destinazione**:  
  
**Sostituisci con**  
Specificare la lunghezza di destinazione per questo mapping. Per il tipo di dati **nvarchar** , ad esempio, è possibile immettere 20 per specificare che il tipo di dati di origine specificato deve essere mappato a **nvarchar (20)**.  
  
