---
title: Creazione di Test case (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a2c1bd3fea167a784d86f7e323566f73c3a01f86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287709"
---
# <a name="creating-test-cases-oracletosql"></a>Creazione di test case (OracleToSQL)
Usare la procedura guidata di Test Case per creare un test. Questa procedura guidata consente di creare test case scegliendo testato e verificato gli oggetti e specificando i parametri di test.  
  
## <a name="starting-the-test-case-wizard"></a>Avvio della procedura guidata di Test Case  
Per avviare Creazione guidata Test Case **nuovo Test Case...**  dal **Tester** menu.  
  
All'avvio, la procedura guidata cerca schema SSMATESTER_ORACLE sul server Oracle di origine. È lo schema di estensione Tester usato per l'archiviazione di oggetti ausiliari. Se il Test Case mpossibile trovare SSMATESTER_ORACLE, visualizza una finestra di dialogo che si propone di creare lo schema. (Questa situazione si verifica in genere durante la prima esecuzione di SSMA Tester)  
  
Se si ottiene la finestra di dialogo, fare clic su **Sì** creare SSMATESTER_ORACLE schema nel server di origine. Si noti che è necessario disporre dei privilegi di Oracle per creare un nuovo utente e creare oggetti nello schema di questo utente.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Panoramica della creazione di Test case usando la procedura guidata  
Il processo di creazione di un test case è costituito da cinque passaggi:  
  
1.  [Initializing Test Cases &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selezione e configurazione degli oggetti da testare &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selezione e configurazione degli oggetti interessati &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizzazione dell'ordine delle chiamate &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Finishing Test Case Preparation &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Test di oggetti di Database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
