---
title: Creazione di Test case (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b3f54a38ae995dd2c83fd36647393f81b802fde2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948457"
---
# <a name="creating-test-cases-sybasetosql"></a>Creazione di test case (SybaseToSQL)
Usare la procedura guidata di Test Case per creare un test. Questa procedura guidata consente di creare test case scegliendo testato e verificato gli oggetti e specificando i parametri di test.  
  
## <a name="starting-the-test-case-wizard"></a>Avvio della procedura guidata di Test Case  
Per avviare Creazione guidata Test Case **nuovo Test Case...**  dal **Tester** menu.  
  
All'avvio, la procedura guidata Cerca database ssmatester2005db o ssmatester2008db (a seconda del tipo di progetto) nel server di Sybase di origine. È lo schema di estensione Tester usato per l'archiviazione di oggetti ausiliari. Se la procedura guidata di Test Case non è possibile trovare ssmatester2005db o ssmatester2008db, visualizza una finestra di dialogo che si propone di creare il database di estensione Tester. (Questa situazione si verifica in genere durante la prima esecuzione di SSMA Tester)  
  
Se si ottiene la finestra di dialogo, fare clic su **Sì** per creare database di Sybase tester nel server di origine. Quindi, verrà visualizzata una finestra di dialogo Nuovo in cui è necessario aggiungere uno o più dispositivi in cui si desidera individuare nuovi Tester database. Fare clic su **Add** per aggiungere un dispositivo. Nel **allocazione dello spazio per il Database di Tester** finestra di dialogo scegliere il dispositivo e specificare la dimensione utilizzata dal database di tester. Inoltre, è possibile impostare il dispositivo separato per i log di database. Si noti che è necessario disporre dei privilegi di Sybase per creare i database.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Panoramica della creazione di Test case usando la procedura guidata  
Il processo di creazione di un test case è costituito da cinque passaggi:  
  
1.  [Inizializzazione di Test case &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Selezione e configurazione degli oggetti da testare &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Selezione e configurazione degli oggetti interessati &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Personalizzazione dell'ordine delle chiamate &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Completamento della preparazione del Test Case &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
