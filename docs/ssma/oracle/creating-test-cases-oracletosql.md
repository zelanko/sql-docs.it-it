---
title: Creazione di test case (OracleToSQL) | Microsoft Docs
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
manager: shamikg
ms.openlocfilehash: 697f7049a60aa7ae2b8c89d1fb6c5ce8e3d29312
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266129"
---
# <a name="creating-test-cases-oracletosql"></a>Creazione di test case (OracleToSQL)
Utilizzare la procedura guidata test case per creare un test. Questa procedura guidata consente di creare test case scegliendo oggetti testati e verificati e specificando i parametri di test.  
  
## <a name="starting-the-test-case-wizard"></a>Avvio della procedura guidata test case  
Per avviare la procedura guidata test case, fare clic su **nuovo test case...** dal menu **tester** .  
  
Quando viene avviata, la procedura guidata cerca SSMATESTER_ORACLE dello schema nel server Oracle di origine. Si tratta dello schema di estensione del tester utilizzato per archiviare gli oggetti ausiliari. Se la procedura guidata test case non riesce a trovare SSMATESTER_ORACLE, viene visualizzata una finestra di dialogo che propone di creare lo schema. Questa situazione si verifica in genere durante la prima esecuzione di SSMA tester.  
  
Se si ottiene la finestra di dialogo, fare clic su **Sì** per creare SSMATESTER_ORACLE schema nel server di origine. Si noti che è necessario disporre dei privilegi Oracle per creare un nuovo utente e creare oggetti nello schema di questo utente.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Panoramica della creazione di test case tramite la procedura guidata  
Il processo di creazione di un test case prevede cinque passaggi:  
  
1.  [Inizializzazione di test case &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selezione e configurazione degli oggetti da testare &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selezione e configurazione degli oggetti interessati &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizzazione dell'ordine delle chiamate &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Completamento della preparazione del test case &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Test di oggetti di database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
