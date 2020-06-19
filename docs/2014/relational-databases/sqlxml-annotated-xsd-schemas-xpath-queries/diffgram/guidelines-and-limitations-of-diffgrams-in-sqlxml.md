---
title: Linee guida e limitazioni di DiffGram in SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f2901f02f8b4a8fc7b77dcb6c1cb166cb6af6ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062945"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Linee guida e limitazioni per i Diffgram in SQLXML
  Quando si utilizzano Diffgram con SQLXML 4.0, tenere presenti le considerazioni seguenti:  
  
-   I tipi di oggetto binario di grandi dimensioni (BLOB), ad esempio i tipi `text/ntext` e le immagini, non devono essere utilizzati nel blocco `<diffgr:before>` quando si utilizzano Diffgram, perché in questo caso verranno inclusi per l'utilizzo nel controllo della concorrenza. Ciò può provocare problemi con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a causa delle limitazioni applicate al confronto per i tipi BLOB. La parola chiave LIKE, ad esempio, viene utilizzata nella clausola WHERE per il confronto tra colonne del tipo di dati `text`. I confronti, tuttavia, hanno esito negativo in presenza di tipi BLOB in cui le dimensioni dei dati sono maggiori di 8K.  
  
-   La presenza di caratteri speciali nei dati `ntext` può provocare problemi con SQLXML 4.0 a causa delle limitazioni applicate al confronto per i tipi BLOB. L'utilizzo, ad esempio, di "[Serializable]" nel blocco `<diffgr:before>` di un Diffgram se utilizzato nel confronto della concorrenza di una colonna di tipo `ntext` avrà esito negativo con la descrizione di errore SQLOLEDB seguente:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
